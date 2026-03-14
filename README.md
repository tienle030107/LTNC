#include <iostream>
using namespace std;

// Yêu cầu 1: Xây dựng cấu trúc Điểm
struct Diem {
    int x, y; // hoành độ và tung độ

    // Quá tải toán tử >> để nhập điểm
    friend istream& operator>>(istream& is, Diem& d) {
        is >> d.x >> d.y;
        return is;
    }

    // Quá tải toán tử << để xuất điểm theo dạng (x,y)
    friend ostream& operator<<(ostream& os, const Diem& d) {
        os << "(" << d.x << "," << d.y << ")";
        return os;
    }

    // Quá tải toán tử == (kiểm tra 2 điểm trùng nhau)
    bool operator==(const Diem& khac) {
        return (this->x == khac.x && this->y == khac.y);
    }

    // Quá tải toán tử < (so sánh kiểu từ điển: x trước, y sau)
    bool operator<(const Diem& khac) {
        if (this->x != khac.x) return this->x < khac.x;
        return this->y < khac.y;
    }

    // Quá tải toán tử + (cộng 2 điểm trả về 1 điểm mới)
    Diem operator+(const Diem& khac) {
        Diem kq;
        kq.x = this->x + khac.x;
        kq.y = this->y + khac.y;
        return kq;
    }
};

// Xây dựng cấu trúc Mảng 1 chiều lưu dãy Điểm
struct MangDiem {
    Diem ds[100];
    int n = 0;

    // Quá tải >> cho mảng điểm
    void nhap() {
        Diem tam;
        while (cin >> tam) {
            ds[n++] = tam;
        }
    }

    // Tìm điểm lớn nhất trong mảng (dùng toán tử < đã nạp chồng)
    Diem timMax() {
        Diem maxD = ds[0];
        for (int i = 1; i < n; i++) {
            if (maxD < ds[i]) { // gọi operator < của Diem
                maxD = ds[i];
            }
        }
        return maxD;
    }

    // Tính tổng tất cả các điểm trong mảng (dùng toán tử + đã nạp chồng)
    Diem tinhTong() {
        Diem tong = ds[0];
        for (int i = 1; i < n; i++) {
            tong = tong + ds[i]; // gọi operator + của Diem
        }
        return tong;
    }
};

int main() {
    // Yêu cầu 2: Viết chương trình nhập vào 1 dãy điểm
    MangDiem mang;
    mang.nhap();

    if (mang.n == 0) return 0;

    // Tìm điểm lớn nhất
    Diem dMax = mang.timMax();

    // Tính tổng điểm
    Diem dTong = mang.tinhTong();

    // Xuất kết quả ra màn hình theo ví dụ
    cout << dMax << endl;
    cout << dTong << endl;

    return 0;
}
