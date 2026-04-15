# Experiment Report: Data Quality Impact on AI Agent

**Student ID:** AI20K-0298
**Name:** Tran Ngoc Huy
**Date:** 2026-04-15

---

## 1. Ket qua thi nghiem

Chay `agent_simulation.py` voi 2 bo du lieu va ghi lai ket qua:

| Scenario | Agent Response | Accuracy (1-10) | Notes |
|----------|----------------|-----------------|-------|
| Clean Data (`processed_data.csv`) | Based on my data, the best choice is Laptop at $1200. | 10 | Du lieu da qua ETL pipeline: loai bo gia am, category rong; ket qua chinh xac |
| Garbage Data (`garbage_data.csv`) | Based on my data, the best choice is Nuclear Reactor at $999999. | 1 | Outlier cuc doan ($999,999) khien Agent chon san pham khong ton tai trong thuc te |

---

## 2. Phan tich & nhan xet

### Tai sao Agent tra loi sai khi dung Garbage Data?

Agent tra loi sai vi `garbage_data.csv` chua nhieu van de chat luong du lieu nghiem trong. Thu nhat, **Duplicate ID**: san pham `Laptop` va `Banana` cung mang ID = 1, gay nham lan khi tra cuu. Thu hai, **Wrong data type**: gia cua `Broken Chair` la chuoi `"ten dollars"` thay vi so, khien phep so sanh gia tri co the bi loi hoan toan. Thu ba, **Extreme Outlier**: `Nuclear Reactor` co gia $999,999 — cao bat thuong so voi cac san pham con lai — nen khi Agent tim san pham co gia cao nhat trong danh muc `electronics`, no chon ngay outlier nay thay vi `Laptop` hop le. Thu tu, **Null values**: `Ghost Item` co ID va category la `None`, gia bang 0, co the gay ra loi `NaN` trong qua trinh xu ly. Ket hop cac loi nay, Agent nhan vao du lieu "doc hai" va dua ra quyet dinh hoan toan sai lech, chung to rang mot AI agent chi tot bang chinh chat luong du lieu no dua vao.

---

## 3. Ket luan

**Quality Data > Quality Prompt?** — Dong y hoan toan.

Du co viet prompt ro rang den dau, neu du lieu dau vao chua outlier, gia tri null, sai kieu du lieu hay ban ghi trung lap, AI agent van se dua ra ket qua sai. Thi nghiem nay cho thay `Nuclear Reactor` thang `Laptop` khong phai vi prompt sai, ma vi du lieu garbage chua outlier $999,999. Chat luong du lieu la nen tang: **Garbage In, Garbage Out** — mot ETL pipeline vung chac voi buoc Validate ky luong la dieu kien tien quyet truoc khi tin tuong bat ky output nao cua AI.
