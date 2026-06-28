# My Exam React Native

แอปดูสินค้าเล็กๆ ที่ทำด้วย Expo, React Native และ TypeScript

## สิ่งที่แอปทำได้

- ดึงข้อมูลสินค้าจาก Fake Store API มาแสดงเป็นลิสต์ (รูป, ชื่อ, ราคา)
- ดึงลิสต์ลงมาเพื่อ refresh ข้อมูลใหม่
- กดที่สินค้าเพื่อดูหน้ารายละเอียด (คำอธิบาย, หมวดหมู่, ราคา)
- กดเพิ่ม/ลบสินค้าจากรายการ Favorite ได้จากหน้ารายละเอียด
- Favorites มีแท็บของตัวเอง และยังคงสถานะอยู่แม้ปิดแอปแล้วเปิดใหม่

## Stack ที่ใช้

- Expo (SDK 56) + expo-router สำหรับ navigation (เป็น file-based routing ที่ build อยู่บน React Navigation)
- TypeScript
- React Context สำหรับเก็บ state ของ favorites แล้ว sync กับ AsyncStorage

## โครงสร้างโปรเจกต์

```
app/
  (tabs)/
    index.tsx        # หน้าลิสต์สินค้า
    favorites.tsx     # หน้า favorites
    _layout.tsx       # ตั้งค่า tab bar
  product/[id].tsx     # หน้ารายละเอียดสินค้า
  _layout.tsx          # root stack + favorites provider
context/
  FavoritesContext.tsx # global favorites state + sync กับ AsyncStorage
types/
  product.ts           # Product type ที่ใช้ร่วมกันทุกหน้า
```

## วิธีรัน

```bash
npm install
npm start
```

จากนั้นสแกน QR code ด้วย Expo Go หรือกด `i`/`a` ใน terminal เพื่อเปิดบน simulator

## หมายเหตุ

- Favorites เก็บเป็น object สินค้าเต็มๆ ไว้ใน AsyncStorage key เดียว ทำให้หน้า favorites ไม่ต้อง fetch ข้อมูลซ้ำ
- หน้ารายละเอียดสินค้าดึงข้อมูลจาก API ด้วย id ตรงๆ แทนที่จะส่งผ่าน navigation params เพื่อให้กด deep link เข้าหน้าสินค้าตรงๆ ก็ยังทำงานได้
