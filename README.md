# solid-pancake#include <string>
#include <iostream>

// สมมติเรียก service ภายนอกหรือไลบรารีตรวจ JWT / X.509
bool verify_token_with_auth_service(const std::string& token) {
    // ทำ HTTP call ไปยัง auth server หรือใช้ไลบรารี JWT เพื่อตรวจ signature/claims
    // ตัวอย่างนี้เป็�� pseudo — ต้องแทนด้วยการเรียกจริง (jwt-cpp, OpenSSL, หรือ HTTP request)
    return token == "valid-token-from-auth"; // ห้ามทำแบบนี้ในจริง
}

int main() {
    std::string token = /* อ่านจาก Authorization header หรือไฟล์ config/secret */ "";
    if (!verify_token_with_auth_service(token)) {
        std::cerr << "ACCESS_DENIED\n";
        return 1;
    }

    // ตรวจ role/claim ว่าเป็น 'pioneer' หรือมี permission ที่จำเป็น
    bool has_pioneer_role = true; // ดึงจาก claims แทน

    if (has_pioneer_role) {
        std::cout << "ACCESS_GRANTED: ผู้บุกเบิก\n";
        // เรียก service ที่มีสิทธิ์จำเพาะผ่าน service account
    } else {
        std::cout << "QUEUED: โปรดรอคิว\n";
        // ส่งข้อความไปยัง queue
    }
    return 0;
}
