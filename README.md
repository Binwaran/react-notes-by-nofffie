# react-notes-by-nofffie
❗**Note 
💡arrow function ใน ( ) => ( ) แบบนี้ มันคือ “การ return ค่าอัตโนมัติ”
const sayHi = () => ("Hi!");

💡แบบมีปีกกา ( ) => {} ต้องเขียน return ด้วยตัวเอง!
const sayHi = () => {
  return "Hi!";
}
💡สูตรจำง่าย ๆ:
(param) => { ... }  มีหลายบรรทัด → ต้องใช้ return
(param) => ( ... )  แค่คืนค่าเดียว → ไม่ต้องใช้ return
(param) => value    ถ้าค่าเดียว (ไม่มี {} หรือ () ก็ได้ในบางกรณี)


## Rendering List Items
โครงสร้างคือ
array.map((item, index) => (
  <Element key={index}>{item}</Element>
));

ตัวอย่างโค้ด
const fruits = ['Apple','Banana','Grape'];

function FruitList() {
  return (
    <ul>
      {fruits.map((fruit, index) => (
        <li key={index}>{fruit}</li>
      ))}
    </ul>
  );
}

✅ อธิบายให้จำง่าย ๆ:
array เป็น กล่อง
.map คือเปิดเอาของออกมาจากกล่อง

กล่อง.map((ชื่อของ, ลำดับของ) => (
  <Element key={ลำดับของ}>{ชื่อของ}</Element>
))

กล่อง.map คือเอากล่องมาเปิด 
มีฟังก์ชั่นในกล่อง สิ่งที่เราต้องรู้คือ ชื่อของและลำดับของ
และให้รีเทิร์นค่าลงใส่ในกล่องเล็กที่มี key= ลำดับของ แปะไว้ ถ้าดูในกล่องเล็กก็จะเห็น "ชื่อของ" อยู่ในนั้น  




