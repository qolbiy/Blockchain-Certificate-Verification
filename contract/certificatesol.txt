// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

/**
 * TOPIK 2 — Blockchain Certificate Verification
 * - Menyimpan hash dokumen sertifikat di blockchain (anti pemalsuan)
 * - Issue (store hash) + Verify (cek validitas)
 */
contract CertificateRegistry {
    address public owner;

    struct Certificate {
        address issuer;
        uint256 issuedAt;
        bool revoked;
        string docType;     // contoh: "Ijazah", "Sertifikat Pelatihan"
        string holderId;    // contoh: NIM / No Peserta (opsional, non-sensitif)
    }

    // hash dokumen (bytes32) => data sertifikat
    mapping(bytes32 => Certificate) private certificates;

    // otorisasi penerbit (mis: admin prodi, panitia, dsb)
    mapping(address => bool) public isIssuer;

    event IssuerAdded(address indexed issuer);
    event IssuerRemoved(address indexed issuer);
    event CertificateIssued(bytes32 indexed docHash, address indexed issuer, uint256 issuedAt);
    event CertificateRevoked(bytes32 indexed docHash, address indexed issuer, uint256 revokedAt);

    modifier onlyOwner() {
        require(msg.sender == owner, "Not owner");
        _;
    }

    modifier onlyIssuer() {
        require(isIssuer[msg.sender], "Not authorized issuer");
        _;
    }

    constructor() {
        owner = msg.sender;
        isIssuer[msg.sender] = true; // deployer otomatis issuer pertama
        emit IssuerAdded(msg.sender);
    }

    function addIssuer(address issuer) external onlyOwner {
        require(issuer != address(0), "Zero address");
        isIssuer[issuer] = true;
        emit IssuerAdded(issuer);
    }

    function removeIssuer(address issuer) external onlyOwner {
        isIssuer[issuer] = false;
        emit IssuerRemoved(issuer);
    }

    /**
     * StoreHash() versi aman:
     * - docHash = SHA-256 dokumen (32 bytes)
     * - docType & holderId hanya metadata ringan (hindari data pribadi sensitif)
     */
    function issueCertificate(
        bytes32 docHash,
        string calldata docType,
        string calldata holderId
    ) external onlyIssuer {
        require(docHash != bytes32(0), "Invalid hash");
        require(certificates[docHash].issuedAt == 0, "Hash already registered");

        certificates[docHash] = Certificate({
            issuer: msg.sender,
            issuedAt: block.timestamp,
            revoked: false,
            docType: docType,
            holderId: holderId
        });

        emit CertificateIssued(docHash, msg.sender, block.timestamp);
    }

    function revokeCertificate(bytes32 docHash) external onlyIssuer {
        Certificate storage c = certificates[docHash];
        require(c.issuedAt != 0, "Not found");
        require(c.issuer == msg.sender, "Only original issuer can revoke");
        require(!c.revoked, "Already revoked");

        c.revoked = true;
        emit CertificateRevoked(docHash, msg.sender, block.timestamp);
    }

    /**
     * Verifikasi berbasis hash:
     * - valid = sudah terdaftar & tidak revoked
     */
    function verifyCertificate(bytes32 docHash)
        external
        view
        returns (
            bool exists,
            bool valid,
            address issuer,
            uint256 issuedAt,
            bool revoked,
            string memory docType,
            string memory holderId
        )
    {
        Certificate memory c = certificates[docHash];
        exists = (c.issuedAt != 0);
        valid = exists && !c.revoked;
        issuer = c.issuer;
        issuedAt = c.issuedAt;
        revoked = c.revoked;
        docType = c.docType;
        holderId = c.holderId;
    }
}
