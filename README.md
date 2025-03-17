#include <iostream>
#include <string>
using namespace std;

class DichVu {
private:
    string MaDV;
    string TenDV;
    double GiaCuoc;
public:
    DichVu() : MaDV(""), TenDV(""), GiaCuoc(0) {}
    void Nhap() {
        cout << "Nhap ma dich vu: ";
        cin >> MaDV;
        cin.ignore();
        cout << "Nhap ten dich vu: ";
        getline(cin, TenDV);
        cout << "Nhap gia cuoc: ";
        cin >> GiaCuoc;
    }
    void Xuat() const {
        cout << "Ma DV: " << MaDV << ", Ten DV: " << TenDV << ", Gia cuoc: " << GiaCuoc << endl;
    }
    double LayGiaCuoc() const {
        return GiaCuoc;
    }
};

class Nguoi {
private:
    string HoTen;
    string DiaChi;
    string SoDT;
public:
    Nguoi() : HoTen(""), DiaChi(""), SoDT("") {}
    void Nhap() {
        cout << "Nhap ho ten: ";
        getline(cin, HoTen);
        cout << "Nhap dia chi: ";
        getline(cin, DiaChi);
        cout << "Nhap so dien thoai: ";
        getline(cin, SoDT);
    }
    void Xuat() const {
        cout << "Ho ten: " << HoTen << ", Dia chi: " << DiaChi << ", So DT: " << SoDT << endl;
    }
};

class KhachHang : public Nguoi {
private:
    int SoLuongDichVu;
    DichVu DV[100];
public:
    KhachHang() : SoLuongDichVu(0) {}
    void Nhap() {
        Nguoi::Nhap();
        cout << "Nhap so luong dich vu da su dung: ";
        cin >> SoLuongDichVu;
        cin.ignore();
        for (int i = 0; i < SoLuongDichVu; i++) {
            cout << "Nhap thong tin dich vu thu " << i + 1 << ":" << endl;
            DV[i].Nhap();
        }
    }
    void Xuat() const {
        Nguoi::Xuat();
        cout << "So luong dich vu da su dung: " << SoLuongDichVu << endl;
        for (int i = 0; i < SoLuongDichVu; i++) {
            cout << "Dich vu thu " << i + 1 << ": ";
            DV[i].Xuat();
        }
    }
    double TongGiaCuoc() const {
        double tong = 0;
        for (int i = 0; i < SoLuongDichVu; i++) {
            tong += DV[i].LayGiaCuoc();
        }
        return tong;
    }
};

int main() {
    cout << "Nhap thong tin mot nguoi:" << endl;
    Nguoi nguoi;
    nguoi.Nhap();
    cout << "\nThong tin nguoi:" << endl;
    nguoi.Xuat();

    cout << "\nNhap thong tin mot khach hang:" << endl;
    KhachHang khachHang;
    khachHang.Nhap();
    cout << "\nThong tin khach hang:" << endl;
    khachHang.Xuat();
    cout << "\nTong gia cuoc khach hang da su dung: " << khachHang.TongGiaCuoc() << endl;

    return 0;
}
