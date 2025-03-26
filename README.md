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

---------------------------------------------------------------------------------------------
สรุปการใช้ useState เบื้องต้น
อันนี้คือลำดับของการใช้ useState ปกติที่เป็นขั้นตอน
1.import { useState } from "react"; ก่อนเสมอ
2.สร้างกล่อง state กับ setState และบอกค่าเริ่มต้น
3.ใช้ onClick เรียก arrow เพื่อบอกว่า setState จะเปลี่ยนค่ายังไง
4.เอาค่าไปโชว์ {state}

อันนี้คือลำดับของการใช้ useState กับ input ที่เป็นขั้นตอน
1.import { useState } from "react"; ก่อนเสมอ
2.สร้างกล่อง state กับ setState และบอกค่าเริ่มต้น
3.กำหนดค่า value={state}
4.ใช้ onChange เรียก arrow เพื่อบอกว่า setState จะเก็บ e.target.value 
5.เอา state ไปโชว์ {state}

---------------------------------------------------------------------------------------------
useState() 
📌 ตัวอย่างที่เจอบ่อยในข้อสอบ
ทำ counter
เก็บ input form
เปลี่ยนข้อความเมื่อคลิก
ซ่อน/แสดงบางอย่าง (toggle show/hide)

Form 
const [state, setState] = useState(initialValue);
* ค่า ใน useState ถ้าเป็นสตริงใส่("") ตัวเลขปกติใส่(0) บูลีนใส่(false)
* array ใส่ ([]) object ใส่ ({})

ตัวอย่างการใช้งาน 
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0); // กำหนดค่าเริ่มต้นเป็น 0
  return (
    <div>
      <p>ตอนนี้นับได้: {count}</p>
      <button onClick={() => setCount(count + 1)}>
        กดเพิ่มค่า
      </button>
    </div>
  );
}

อธิบาย
สิ่งแรงคือต้อง import {useState} from "react"; ก่อนเสมอ

const [count, setCount] = useState(0);
ให้อาเรย์นี้เหมือนกล่องขนมที่มีบอกว่า มีขนมกี่อัน(count) และวิธีใส่ขนมเข้าในกล่อง(setCount) *แต่ต้องผ่านมือเรา และกำหนดว่า ตอนแรกกล่องนี้ไม่มีขนม(0)
ใน return จะเอามาโชว์ว่ามีขนมกี่อัน ก็ให้ใช้ {count} 
ตามตัวอย่าง ปุ่มนี้บอกว่า เมื่อคลิก จะมีฟังชั่น arrow อันนึง จะบอกวิธีการ(setCount)
วิธีการนี้จะวงเล็บบอกเราว่าให้เอาขนมมาทำอะไร ในที่นี้คือให้เอาขนมบวกเพิ่มเข้าไปทีละ 1

สรุป useState 
1. มันเป็นกล่องขนม [มีกี่อัน, วิธีการกระทำ] ตอนแรกกำหนดให้เป็นอะไร
2. เวลาใช้ โชว์ว่ามีกี่อัน {ขนมกี่อัน}
3. บอกวิธีการกระทำ ให้ arrow บอก วิธีการกระทำ ว่าจะทำยังไง
   
---------------------------------------------------------------------------------------------
กรณีที่ เป็นแบบฟอร์มหลายช่อง
import { useState } from "react";

function FormExample() {
  const [name, setName] = useState("");     // state สำหรับชื่อ
  const [email, setEmail] = useState("");   // state สำหรับอีเมล

  return (
    <div>
      <input 
        type="text" 
        value={name}
        onChange={(e) => setName(e.target.value)} 
        placeholder="ชื่อของเธอ" />
      <input 
        type="email" 
        value={email}
        onChange={(e) => setEmail(e.target.value)} 
        placeholder="อีเมล" 
      />
      <p>สวัสดี {name} จ้า! เราจะส่งเมลไปที่ {email} นะจ๊ะ</p>
    </div>
  );
}

🧠 อธิบาย:
e.target.value หรือ event.target.value ค่าแบบมาตรฐาน ที่เราต้องใช้เมื่ออยากรู้ว่าใน <input> ผู้ใช้พิมพ์อะไรลงไป
e.target.value นิยมใช้กับ onChange มากที่สุด นี่คือ Pattern มาตรฐานของ React
เพราะ onChange = เหตุการณ์ที่ผู้ใช้ "เปลี่ยนค่า" อะไรบางอย่าง (พิมพ์, เลือก, แก้ไข ฯลฯ)
✅ ถ้าใช้ useState ควบคุม input ก็ต้องใส่ value={state} เสมอ! (เช่น value={name})

✅ e.target.value ใช้เมื่อ:
ผู้ใช้ "พิมพ์" หรือ "เลือก" ค่าบางอย่างในฟอร์ม เช่น:
1.<input>
2.<textarea>
3.<select>
<input onChange={(e) => setName(e.target.value)} />
<textarea onChange={(e) => setBio(e.target.value)} />
<select onChange={(e) => setCountry(e.target.value)}></select>


การใช้งาน
เขียนแบบแยก function ไปเลยก็ได้ เช่น:
function handleNameChange(event) {
  setName(event.target.value);
}

เวลาใช้ก็แค่ เรียกใช้ฟังก์ชั่น <input onChange={handleNameChange} />
❗ ถ้าไม่ใส่ e.target.value จะเป็นยังไง?
ก็เหมือนแม่บอกลูกว่าให้เก็บเงินไว้ แล้วลูกตอบมาว่า “เก็บแล้วค่ะ” …แต่ไม่ได้บอกว่าเก็บไว้ที่ไหน! 😩
React จะงงว่าเอาค่าจากไหนมาอัปเดต state จ้าาา



---------------------------------------------------------------------------------------------
ตัวอย่าง Show/Hide toggle + ข้อมูล

function Profile() {
  const [isVisible, setIsVisible] = useState(false); // ซ่อนหรือโชว์
  const [username, setUsername] = useState("Adam"); // ชื่อผู้ใช้

  return (
    <div>
      <button onClick={() => setIsVisible(!isVisible)}>
        {isVisible ? "ซ่อน" : "แสดง"} โปรไฟล์
      </button>

      {isVisible && <p>ชื่อของฉันคือ {username}</p>}
    </div>
  );
}

โค้ดนี้เป็นการ กดปุ่มเพื่อสลับโชว์/ซ่อนข้อความ ด้วยการใช้ useState
const [isVisible, setIsVisible] = useState(false);
💥 เอาไว้บอกว่า “ตอนนี้จะแสดงโปรไฟล์มั้ย?” เริ่มต้นคือควรเซ็ทค่าเป็น false = ยังไม่โชว์

const [username, setUsername] = useState("Adam");
💖 เก็บชื่อผู้ใช้ไว้โชว์ตอนกดดูโปรไฟล์ (ใส่ชื่อค่าเริ่มต้นเป็น Adam หรือไม่ใส่ก็ได้)

<button onClick={() => setIsVisible(!isVisible)}>
  {isVisible ? "ซ่อน" : "แสดง"} โปรไฟล์
</button>
👆 ปุ่มนี้คือ Highlight!!
ทุกครั้งที่กด → setIsVisible(!isVisible) → สลับค่า true/false
แล้วข้อความในปุ่มก็จะเปลี่ยนระหว่าง “แสดง” กับ “ซ่อน” โดยใช้ ternary operator จ้า
มันคือการบอกว่า วิธีการเปลี่ยนค่า คือ ไม่ให้เป็นค่าเดิม

{isVisible && <p>ชื่อของฉันคือ {username}</p>}
💡 ถ้า isVisible === true → โชว์ <p>
ถ้า false → React จะ ไม่ render อะไรเลย
คำสั่งนี้เรียกว่า Conditional Rendering


---------------------------------------------------------------------------------------------
ตัวอย่าง เปลี่ยนข้อความเมื่อคลิก
import { useState } from "react";

function ToggleMessage() {
  const [message, setMessage] = useState("ยังไม่ได้กดเลยจ้า");

  const handleClick = () => {
    setMessage("กดแล้วนะยะ!! 💥");
  };

  return (
    <div>
      <p>{message}</p>
      <button onClick={handleClick}>
        คลิกสิจ๊ะ
      </button>
    </div>
  );
}
🧠 อธิบายทีละจุด:
const [message, setMessage] = useState("ยังไม่ได้กดเลยจ้า");
💡 คือประกาศตัวแปร message สำหรับเก็บข้อความ
👉 ค่าเริ่มต้นคือ "ยังไม่ได้กดเลยจ้า"

const handleClick = () => {
  setMessage("กดแล้วนะยะ!! 💥");
};
🖐 นี่คือฟังก์ชันที่ทำงานตอนกดปุ่ม
✨ เมื่อกด จะเปลี่ยนค่า message เป็น "กดแล้วนะยะ!! 💥"

<p>{message}</p>
🧾 แสดงข้อความตามที่อยู่ในตัวแปร message


---------------------------------------------------------------------------------------------
ถ้าอยากเปลี่ยนสลับข้อความไปมา (Toggle)
function ToggleText() {
  const [clicked, setClicked] = useState(false);

  const handleClick = () => {
    setClicked(!clicked); // สลับ true <-> false
  };

  return (
    <div>
      <p>{clicked ? "กดแล้วจ้า!" : "ยังไม่ได้กดเลยนะ!"}</p>
      <button onClick={handleClick}>
        คลิกเพื่อเปลี่ยนข้อความ
      </button>
    </div>
  );
}
🧠 เคล็ดลับ:
เวลาอยากให้ ข้อความเปลี่ยน → ใส่เงื่อนไขใน JSX ได้เลย เช่น {condition ? A : B}
ใช้ state เป็น boolean ก็ง่ายมากในการ toggle อะไรไปมา


---------------------------------------------------------------------------------------------
🎯 ตัวอย่างมากกว่า 2 state
🎯 ตัวอย่าง: แบบฟอร์มกรอกชื่อ + อีเมล + กด Like แล้วโชว์ผล
import { useState } from "react";

function UserProfileForm() {
  const [name, setName] = useState("");         // ชื่อ
  const [email, setEmail] = useState("");       // อีเมล
  const [likes, setLikes] = useState(0);        // จำนวนคนกด Like

  const handleLike = () => {
    setLikes(likes + 1);
  };

  return (
    <div>
      <h2>ฟอร์มลงทะเบียน</h2>
      
      <input 
        type="text" 
        value={name}
        onChange={(e) => setName(e.target.value)}
        placeholder="ป้อนชื่อของเธอ"
      />

      <br />

      <input 
        type="email" 
        value={email}
        onChange={(e) => setEmail(e.target.value)}
        placeholder="ป้อนอีเมลของเธอ"
      />

      <br /><br />

      <button onClick={handleLike}>❤️ ถูกใจ {likes} ครั้ง</button>

      <hr />

      <h3>ข้อมูลของเธอ</h3>
      <p>ชื่อ: {name}</p>
      <p>อีเมล: {email}</p>
    </div>
  );
}

🛑 ถามว่าใช้ object แทนได้มั้ย? ได้... แต่ จะยุ่งมาก เช่น:
const [form, setForm] = useState({ name: "", email: "" });
setForm({ ...form, name: "ใหม่" });

onChange={(e) => setEmail(e.target.value)}
✅ "ถ้าใช้ onChange แล้วต้องการดึงค่าจาก input → ต้องใส่ e เสมอ!"
แต่ถ้าใช้ onChange แล้ว ไม่ได้แตะต้องอะไรจาก event ก็ไม่ต้องใส่ e ก็ได้ (แต่…นาน ๆ เจอสถานการณ์นี้ที)


---------------------------------------------------------------------------------------------
💥 เรื่องของ “การส่งค่าไปมาหากัน” ระหว่าง state หรือระหว่างคอมโพเนนต์ มันคือเรื่องใหญ่ของ React ที่ออกสอบบ่อย! 📚🔥
🧠 แบบที่ 1: ส่งค่าระหว่าง state ภายในคอมโพเนนต์เดียว (มีความสัมพันธ์กัน)
🎯 ตัวอย่าง: กดเลือกสินค้าชิ้นนึง แล้วให้ชื่อ + ราคา เปลี่ยนตาม
import { useState } from "react";

function ProductSelector() {
  const [selectedProduct, setSelectedProduct] = useState("apple");
  const [price, setPrice] = useState(1.2); // default ราคาของ apple

  const handleChange = (e) => {
    const product = e.target.value;
    setSelectedProduct(product);

    // update price ตามสินค้าที่เลือก
    if (product === "apple") setPrice(1.2);
    else if (product === "banana") setPrice(0.8);
    else if (product === "mango") setPrice(1.5);
  };

  return (
    <div>
      <select value={selectedProduct} onChange={handleChange}>
        <option value="apple">🍎 Apple</option>
        <option value="banana">🍌 Banana</option>
        <option value="mango">🥭 Mango</option>
      </select>

      <p>สินค้าที่เลือก: {selectedProduct}</p>
      <p>ราคาต่อชิ้น: ${price}</p>
    </div>
  );
}

const [selectedProduct, setSelectedProduct] = useState("apple");
const [price, setPrice] = useState(1.2);
💬 เก็บชื่อสินค้าและราคาปัจจุบันไว้

const handleChange = (e) => {
  const product = e.target.value;
  setSelectedProduct(product);
🎯 เมื่อผู้ใช้เปลี่ยนสินค้า → ก็อัปเดตทั้งชื่อและราคาใหม่
✅ การประกาศตัวแปรแยกไว้จะทำให้โค้ดอ่านง่ายขึ้น!



---------------------------------------------------------------------------------------------
🧠 แบบที่ 2: ส่งค่าข้ามคอมโพเนนต์ Parent ↔ Child
🎯 ตัวอย่าง: พ่อส่งฟังก์ชันให้ลูก แล้วลูกกดปุ่มเพื่อบอกพ่อว่า “ฉันเลือกอะไรจ๊ะพ่อ!”
// Parent.jsx
import { useState } from "react";
import Child from "./Child";

function Parent() {
  const [selectedColor, setSelectedColor] = useState("");

  const handleColorChange = (newColor) => {
    setSelectedColor(newColor);
  };

  return (
    <div>
      <h2>แม่เลือกสี: {selectedColor}</h2>
      <Child onColorSelect={handleColorChange} />
    </div>
  );
}

export default Parent;

🎓 เทคนิคจำ:
“แม่เก็บ state — ลูกเรียกใช้” 💅
ถ้า state อยู่ที่แม่ → แม่ต้องส่งฟังก์ชันไปให้ลูกใช้
แล้วลูกก็ส่งค่ากลับมาอัปเดตแม่ โดยใช้ฟังก์ชันนั้นแหละลูก!


---------------------------------------------------------------------------------------------
🎯 เคส: แบบฟอร์มลงทะเบียนพร้อม Preview ทันที
ใช้ useState หลายตัว, มีความสัมพันธ์กัน, ส่งค่าระหว่างคอมโพเนนต์, และเชื่อมโยง action ไปมาระหว่างแม่ลูก!!

โครงสร้าง
-Parent (RegisterForm)
  -มี state รวมทุกอย่าง
  -ส่งข้อมูล + ฟังก์ชันไปให้ลูก
Child (FormInputs)
  -มี input หลายตัว → เวลาเปลี่ยนจะอัปเดต parent
Child (Preview)
  -แสดงผลสิ่งที่กรอกทันทีแบบ real-time

✅ โค้ด: RegisterForm.jsx (แม่)
import { useState } from "react";
import FormInputs from "./FormInputs";
import Preview from "./Preview";

function RegisterForm() {
  const [form, setForm] = useState({
    name: "",
    email: "",
    gender: "",
    agree: false
  });

  const handleChange = (field, value) => {
    setForm((prev) => ({
      ...prev,
      [field]: value
    }));
  };

  return (
    <div>
      <h2>ฟอร์มลงทะเบียนสุดปัง 💅</h2>
      <FormInputs form={form} onChange={handleChange} />
      <Preview form={form} />
    </div>
  );
}

export default RegisterForm;

✅ โค้ด: FormInputs.jsx (ลูกคนที่ 1 - กรอกข้อมูล)
function FormInputs({ form, onChange }) {
  return (
    <div>
      <input 
        type="text"
        value={form.name}
        onChange={(e) => onChange("name", e.target.value)}
        placeholder="ชื่อของเธอ"
      /><br/>

      <input 
        type="email"
        value={form.email}
        onChange={(e) => onChange("email", e.target.value)}
        placeholder="อีเมล"
      /><br/>

      <select 
        value={form.gender}
        onChange={(e) => onChange("gender", e.target.value)}
      >
        <option value="">--เลือกเพศ--</option>
        <option value="หญิง">หญิง</option>
        <option value="ชาย">ชาย</option>
        <option value="อื่น ๆ">อื่น ๆ</option>
      </select><br/>

      <label>
        <input 
          type="checkbox"
          checked={form.agree}
          onChange={(e) => onChange("agree", e.target.checked)}
        />
        ยอมรับเงื่อนไข
      </label>
    </div>
  );
}

export default FormInputs;

✅ โค้ด: Preview.jsx (ลูกคนที่ 2 - แสดงข้อมูล)
function Preview({ form }) {
  return (
    <div style={{ marginTop: "20px" }}>
      <h3>👁‍🗨 พรีวิวข้อมูลที่กรอก:</h3>
      <p>ชื่อ: {form.name || "ยังไม่ได้กรอก"}</p>
      <p>อีเมล: {form.email || "ยังไม่ได้กรอก"}</p>
      <p>เพศ: {form.gender || "ยังไม่ได้เลือก"}</p>
      <p>
        เงื่อนไข: {form.agree ? "✅ ยอมรับแล้ว" : "❌ ยังไม่ยอมรับ"}
      </p>
    </div>
  );
}

export default Preview;


--------------------------------------------------------------------------

💡 Form Handling การควบคุมค่าจาก input form ต่าง ๆ 
แล้วเก็บค่าพวกนั้นลงใน state ด้วย useState
เพื่อให้เรา จัดการข้อมูล ได้เองแบบ 100%
Standard Form
import { useState } from "react";

function SimpleForm() {
  const [name, setName] = useState("");

  const handleSubmit = (e) => {
    e.preventDefault(); // กันหน้ารีเฟรช
    alert(`ชื่อที่กรอกคือ: ${name}`);
  };

  return (
    <form onSubmit={handleSubmit}>
      <label>
        ชื่อของเธอ:
        <input 
          type="text" 
          value={name}
          onChange={(e) => setName(e.target.value)} 
        />
      </label>
      <button type="submit">ส่งข้อมูล</button>
    </form>
  );
}

**onChange={(e) => setName(e.target.value)} 
ทุกครั้งที่พิมพ์ → อัปเดต state
🧠 สรุปแนวคิด "Form Controlled Components"
"React คุมทุกอย่างเอง"
→ React จะ ไม่ปล่อยให้ input เปลี่ยนค่าเอง
→ เราต้องใช้ state เก็บไว้เสมอ

✅ เมื่อไหร่ต้องใช้ e.preventDefault()?  เมื่อเราใช้ <form> แล้วมีปุ่ม type="submit"

---------------------------------------------------------------------------------------------
🎯 Form หลายช่อง
function MultiForm() {
  const [form, setForm] = useState({
    username: "",
    email: ""
  });

  const handleChange = (e) => {
    const { name, value } = e.target;
    setForm((prev) => ({ ...prev, [name]: value }));
  };

  const handleSubmit = (e) => {
    e.preventDefault();
    console.log(form); // ได้ทั้ง username และ email
  };

  return (
    <form onSubmit={handleSubmit}>
      <input 
        name="username"
        value={form.username}
        onChange={handleChange}
        placeholder="Username"
      />
      <input 
        name="email"
        value={form.email}
        onChange={handleChange}
        placeholder="Email"
      />
      <button type="submit">Submit</button>
    </form>
  );
}

✅ จุดที่ออกสอบบ่อย:
เขียนฟังก์ชัน handleChange() แบบ dynamic
คุม checkbox, radio, select
e.preventDefault() สำคัญมาก!
controlled vs uncontrolled (เน้น controlled)
เก็บค่าทุกช่องใน state object เดียว

💅 เคล็ดลับ:
ถ้า input มีหลายตัว → ใช้ name ของ input เป็น key แล้ว setForm แบบ object จะสวยและควบคุมง่ายกว่า 💻

---------------------------------------------------------------------------------------------
👑 แบบฟอร์มมหาชน พร้อม Validation ครบสูตร
import { useState } from "react";

function FullForm() {
  const [form, setForm] = useState({
    name: "",
    email: "",
    agree: false,
    gender: ""
  });

  const [errors, setErrors] = useState({});

  const handleChange = (e) => {
    const { name, value, type, checked } = e.target;

    setForm((prev) => ({
      ...prev,
      [name]: type === "checkbox" ? checked : value
    }));
  };

  const validate = () => {
    const newErrors = {};

    if (!form.name.trim()) {
      newErrors.name = "ชื่อห้ามเว้นว่าง!";
    }

    if (!form.email.includes("@")) {
      newErrors.email = "อีเมลไม่ถูกต้อง!";
    }

    if (!form.gender) {
      newErrors.gender = "กรุณาเลือกเพศ!";
    }

    if (!form.agree) {
      newErrors.agree = "ต้องยอมรับเงื่อนไขก่อน!";
    }

    setErrors(newErrors);
    return Object.keys(newErrors).length === 0;
  };

  const handleSubmit = (e) => {
    e.preventDefault();
    if (validate()) {
      alert("ส่งข้อมูลสำเร็จ!! 🎉");
      console.log("📦 ข้อมูลที่ส่ง:", form);
    } else {
      alert("มีบางอย่างผิดพลาดนะจ๊ะ 😱");
    }
  };

  return (
    <form onSubmit={handleSubmit}>
      <h2>🌟 ฟอร์มลงทะเบียนสุดปัง 🌟</h2>

      <label>
        ชื่อ:
        <input
          type="text"
          name="name"
          value={form.name}
          onChange={handleChange}
        />
        {errors.name && <span style={{ color: "red" }}>{errors.name}</span>}
      </label>
      <br />

      <label>
        อีเมล:
        <input
          type="email"
          name="email"
          value={form.email}
          onChange={handleChange}
        />
        {errors.email && <span style={{ color: "red" }}>{errors.email}</span>}
      </label>
      <br />

      <label>
        เพศ:
        <select
          name="gender"
          value={form.gender}
          onChange={handleChange}
        >
          <option value="">-- เลือกเพศ --</option>
          <option value="หญิง">หญิง</option>
          <option value="ชาย">ชาย</option>
          <option value="อื่น ๆ">อื่น ๆ</option>
        </select>
        {errors.gender && <span style={{ color: "red" }}>{errors.gender}</span>}
      </label>
      <br />

      <label>
        <input
          type="checkbox"
          name="agree"
          checked={form.agree}
          onChange={handleChange}
        />
        ยอมรับเงื่อนไขและข้อตกลง
        {errors.agree && <span style={{ color: "red" }}>{errors.agree}</span>}
      </label>
      <br />

      <button type="submit">✨ ส่งข้อมูล ✨</button>
    </form>
  );
}

🔍 สิ่งที่แบบฟอร์มนี้ทำ (และสอบชอบมาก!)
เรื่องที่เจอในข้อสอบ	มีในโค้ดนี้มั้ย?
Form Controlled	✅ มีครบ
Checkbox Handling	✅ มี
Select Dropdown	✅ มี
Validation / Error	✅ มี
ใช้ state แยกเก็บ	✅ มี
ใช้ preventDefault()	✅ มี
โชว์ข้อความ Error แบบ Real-Time	✅ มี


✅ เคล็ดลับจำไว้สอบ
"ถ้า form มีหลายช่อง → ใช้ name เป็น key"
"ถ้ามี error → เก็บไว้ใน errors object แล้วโชว์ใต้ช่องนั้นเลย"
"form ที่ดี = ผูก input กับ state เสมอ (controlled)"

---------------------------------------------------------------------------
เรื่อง Manipulating array state
💡 สรุปภาพรวมก่อน
React ไม่ให้เราแก้ไข array ตรง ๆ แบบ arr.push() เด้อออ ❌
ต้อง "สร้าง array ใหม่" แล้วใช้ setState() ใส่เข้าไป

✨ เคส 1: เพิ่ม item เข้าไปใน array
import { useState } from "react";

function AddItemExample() {
  const [items, setItems] = useState([]);

  const addItem = () => {
    const newItem = prompt("กรอกชื่อ item:");
    if (newItem) {
      setItems([...items, newItem]); // เพิ่มท้าย
    }
  };

  return (
    <div>
      <button onClick={addItem}>➕ เพิ่มรายการ</button>
      <ul>
        {items.map((item, index) => (
          <li key={index}>• {item}</li>
        ))}
      </ul>
    </div>
  );
}


---------------------------------------------------------------------------------------------
✨ เคส 2: ลบ item จาก array
const deleteItem = (indexToRemove) => {
  setItems(items.filter((_, index) => index !== indexToRemove));
};
ใช้ใน map แบบนี้:
{items.map((item, index) => (
  <li key={index}>
    {item} <button onClick={() => deleteItem(index)}>❌ ลบ</button>
  </li>
))}

✨ เคส 3: แก้ไข item ใน array
const editItem = (indexToEdit) => {
  const newItem = prompt("แก้ไขชื่อ:");
  if (newItem) {
    const newArray = items.map((item, index) =>
      index === indexToEdit ? newItem : item
    );
    setItems(newArray);
  }
};


🧠 สรุปคำสั่งเด็ดในการ manipulate array state
การกระทำ	วิธีที่ใช้
เพิ่มท้าย	[...items, newItem]
เพิ่มหน้า	[newItem, ...items]
ลบ	filter()
แก้ไข	map()
เคลียร์หมด	setItems([])

✅ เคล็ดลับจำ:
ทุกครั้งที่แก้ array → ให้สร้าง array ใหม่เสมอ (copy แล้วแก้)


---------------------------------------------------------------------------------------------
✅ โค้ด: Todo List แบบ CRUD เต็มระบบ
import { useState } from "react";

function TodoList() {
  const [todos, setTodos] = useState([]);
  const [newTodo, setNewTodo] = useState("");
  const [editingIndex, setEditingIndex] = useState(null);
  const [editingText, setEditingText] = useState("");

  const addTodo = () => {
    if (newTodo.trim() === "") return;
    setTodos([...todos, newTodo]);
    setNewTodo("");
  };

  const deleteTodo = (index) => {
    setTodos(todos.filter((_, i) => i !== index));
  };

  const startEdit = (index) => {
    setEditingIndex(index);
    setEditingText(todos[index]);
  };

  const cancelEdit = () => {
    setEditingIndex(null);
    setEditingText("");
  };

  const saveEdit = () => {
    if (editingText.trim() === "") return;
    const updated = todos.map((item, index) =>
      index === editingIndex ? editingText : item
    );
    setTodos(updated);
    cancelEdit();
  };

  return (
    <div>
      <h2>📝 Todo List CRUD</h2>

      <input
        value={newTodo}
        onChange={(e) => setNewTodo(e.target.value)}
        placeholder="เพิ่มงานที่ต้องทำ"
      />
      <button onClick={addTodo}>➕ เพิ่ม</button>

      <ul>
        {todos.map((todo, index) => (
          <li key={index}>
            {editingIndex === index ? (
              <>
                <input
                  value={editingText}
                  onChange={(e) => setEditingText(e.target.value)}
                />
                <button onClick={saveEdit}>💾 บันทึก</button>
                <button onClick={cancelEdit}>❌ ยกเลิก</button>
              </>
            ) : (
              <>
                {todo}
                <button onClick={() => startEdit(index)}>✏️ แก้</button>
                <button onClick={() => deleteTodo(index)}>🗑️ ลบ</button>
              </>
            )}
          </li>
        ))}
      </ul>
    </div>
  );
}

💡 จุดที่ออกสอบชัวร์ในโค้ดนี้:
ฟีเจอร์	คำอธิบาย
✅ Create	พิมพ์ + ปุ่มเพิ่ม → บันทึกเข้า array
✅ Read	map รายการ todo ทั้งหมด
✅ Update	แก้ข้อความ → ปุ่ม save
✅ Delete	ลบรายการด้วย filter()
✅ State หลายตัว	เก็บ todo, ข้อความใหม่, ข้อความกำลังแก้, index

👑 เคล็ดลับจำสูตร CRUD:
➕ Create → setTodos([...todos, newTodo])
📖 Read → todos.map(...)
✏️ Update → map() แล้วเช็ค index
🗑️ Delete → filter() เอา index ออก


---------------------------------------------------------------------------------------------
✅ Shopping Cart CRUD (Add / Update Qty / Delete / Total Price)
import { useState } from "react";

function ShoppingCart() {
  const [cart, setCart] = useState([]);

  const addItem = (product) => {
    const existingIndex = cart.findIndex((item) => item.id === product.id);

    if (existingIndex !== -1) {
      // ถ้ามีอยู่แล้ว เพิ่มจำนวน
      const updatedCart = cart.map((item, index) =>
        index === existingIndex
          ? { ...item, quantity: item.quantity + 1 }
          : item
      );
      setCart(updatedCart);
    } else {
      // ถ้ายังไม่มี เพิ่มเข้าใหม่
      setCart([...cart, { ...product, quantity: 1 }]);
    }
  };

  const updateQty = (index, amount) => {
    const newCart = [...cart];
    newCart[index].quantity += amount;

    // ถ้าจำนวน <= 0 ลบเลย
    if (newCart[index].quantity <= 0) {
      deleteItem(index);
    } else {
      setCart(newCart);
    }
  };

  const deleteItem = (index) => {
    setCart(cart.filter((_, i) => i !== index));
  };

  const total = cart.reduce(
    (sum, item) => sum + item.price * item.quantity,
    0
  );

  // สินค้าให้เลือก
  const products = [
    { id: 1, name: "🍎 Apple", price: 1.2 },
    { id: 2, name: "🍌 Banana", price: 0.8 },
    { id: 3, name: "🥭 Mango", price: 1.5 },
  ];

  return (
    <div>
      <h2>🛍️ ร้านผลไม้ React</h2>

      <h3>🍒 สินค้า:</h3>
      {products.map((product) => (
        <div key={product.id}>
          {product.name} - ${product.price.toFixed(2)}
          <button onClick={() => addItem(product)}>🛒 เพิ่มใส่ตะกร้า</button>
        </div>
      ))}

      <hr />

      <h3>🧺 ตะกร้าของเธอ</h3>
      {cart.length === 0 ? (
        <p>ยังไม่มีสินค้าในตะกร้า</p>
      ) : (
        <ul>
          {cart.map((item, index) => (
            <li key={item.id}>
              {item.name} - ${item.price} × {item.quantity} ={" "}
              <strong>${(item.price * item.quantity).toFixed(2)}</strong>
              <button onClick={() => updateQty(index, 1)}>➕</button>
              <button onClick={() => updateQty(index, -1)}>➖</button>
              <button onClick={() => deleteItem(index)}>❌ ลบ</button>
            </li>
          ))}
        </ul>
      )}

      <h3>💰 ยอดรวมทั้งหมด: ${total.toFixed(2)}</h3>
    </div>
  );
}

📚 อธิบายสิ่งที่ครอบจักรวาล:
ฟีเจอร์	ใช้เทคนิคอะไร
✅ Add	findIndex() แล้วใช้ map() หรือ push
✅ Update Qty	map() แก้จำนวน
✅ Delete	filter()
✅ Total Price	reduce() หาผลรวม
✅ Object ใน array	ใช้ id, name, price, quantity

👑 สอบออกแน่!
เพิ่มสินค้าด้วยเงื่อนไขว่า “ถ้ามีอยู่แล้วต้องเพิ่มจำนวน ไม่เพิ่มซ้ำ”
ใช้ map, filter, reduce ครบ!
เขียนการคำนวณยอดรวมแบบ real-time

---------------------------------------------------------------------------
Data Fetching คือ?
คือการ “ดึงข้อมูลจากแหล่งอื่น (API, ฐานข้อมูล, mock server ฯลฯ)”
แล้วเอาข้อมูลนั้นมาแสดงในหน้าเว็บ ผ่านการใช้ state

✅ โค้ดตัวอย่าง: Fetch ข้อมูลแบบง่ายจาก API
import { useEffect, useState } from "react";

function FetchUser() {
  const [users, setUsers] = useState([]);
  const [loading, setLoading] = useState(true); // เช็คว่าโหลดเสร็จยัง

  useEffect(() => {
    fetch("https://jsonplaceholder.typicode.com/users")
      .then((res) => res.json())
      .then((data) => {
        setUsers(data);
        setLoading(false);
      })
      .catch((err) => {
        console.error("เกิดข้อผิดพลาดจ้า!", err);
        setLoading(false);
      });
  }, []); // 👈 ใส่ [] เพื่อให้ fetch แค่รอบเดียวตอนโหลด

  return (
    <div>
      <h2>📡 ผู้ใช้งานจาก API</h2>
      {loading ? (
        <p>⏳ กำลังโหลดข้อมูล...</p>
      ) : (
        <ul>
          {users.map((user) => (
            <li key={user.id}>
              👤 {user.name} - 📧 {user.email}
            </li>
          ))}
        </ul>
      )}
    </div>
  );
}

🔍 คำอธิบายเด็ด ๆ:
องค์ประกอบ	ทำหน้าที่
useEffect()	รันโค้ดตอน component mount (โหลดครั้งแรก)
fetch(...)	ดึงข้อมูลจาก API
res.json()	แปลง response เป็น JSON
setUsers(data)	เก็บข้อมูลเข้า state
loading	เช็คว่าโหลดเสร็จหรือยัง

📦 โจทย์สอบที่ชอบออก:
ให้เขียน component ดึงข้อมูลจาก API
ให้แสดง loading ระหว่างโหลด
ให้แสดง error ถ้าดึงไม่ได้
ให้ใส่ useEffect อย่างถูกต้อง (บางคนลืม [] แล้ว loop ตายทั้ง component 😭)

✅ เคล็ดลับจำ:
useEffect(() => { fetch... }, [])
คือสูตรดึงข้อมูลครั้งเดียวตอนโหลด component
ถ้าไม่ใส่ [] → มันจะ fetch ทุกครั้งที่ rerender → พัง!

---------------------------------------------------------------------------------------------
💡 Axios คืออะไร?
เป็นไลบรารีสำหรับดึงข้อมูลแบบ HTTP (เหมือน fetch)
แต่ใช้ ง่ายกว่า / จัดการ error ดีกว่า / เขียนสั้นกว่า / ส่ง header ได้สะดวกกว่า
✅ ติดตั้งก่อน (สำคัญมาก)
npm install axios

✨ โค้ดตัวอย่าง: ใช้ Axios ดึงข้อมูล (GET)
import { useEffect, useState } from "react";
import axios from "axios";

function AxiosExample() {
  const [posts, setPosts] = useState([]);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    axios
      .get("https://jsonplaceholder.typicode.com/posts")
      .then((res) => {
        setPosts(res.data);
        setLoading(false);
      })
      .catch((err) => {
        console.error("เกิดข้อผิดพลาดแม่!", err);
        setLoading(false);
      });
  }, []);

  return (
    <div>
      <h2>📰 บทความจาก API (Axios)</h2>
      {loading ? (
        <p>⏳ กำลังโหลดจ้า...</p>
      ) : (
        <ul>
          {posts.slice(0, 5).map((post) => (
            <li key={post.id}>
              <strong>{post.title}</strong>
              <p>{post.body}</p>
            </li>
          ))}
        </ul>
      )}
    </div>
  );
}


✨ Syntax Axios CRUD ที่ต้องจำ
ชนิด	Axios Code
GET    axios.get(url)
POST   axios.post(url, data)
PUT    axios.put(url, data)
DELETE axios.delete(url)

✅ ตัวอย่าง: Real-time Search ด้วย Axios
🎯 สิ่งที่เราจะทำ:
พิมพ์ใน Search Bar → ส่งค่าไปหาข้อมูลจาก API (Axios)
แสดงผลลัพธ์ที่ตรงกับคำค้นแบบทันที
ดัก Loading / Error ครบสูตร!

ใช้ API จาก https://jsonplaceholder.typicode.com/users
พิมพ์ชื่อ แล้วกรองชื่อผู้ใช้ที่ตรงกับ keyword แบบสด ๆ

import { useState, useEffect } from "react";
import axios from "axios";

function RealTimeSearch() {
  const [query, setQuery] = useState("");
  const [results, setResults] = useState([]);
  const [loading, setLoading] = useState(false);

  // ใช้ useEffect ให้ดึงข้อมูลทุกครั้งที่ query เปลี่ยน
  useEffect(() => {
    if (query.trim() === "") {
      setResults([]);
      return;
    }

    setLoading(true);

    const timer = setTimeout(() => {
      axios
        .get("https://jsonplaceholder.typicode.com/users")
        .then((res) => {
          // กรองข้อมูลจาก API ด้วย query ที่ผู้ใช้พิมพ์
          const filtered = res.data.filter((user) =>
            user.name.toLowerCase().includes(query.toLowerCase())
          );
          setResults(filtered);
          setLoading(false);
        })
        .catch((err) => {
          console.error("Error fetching data", err);
          setLoading(false);
        });
    }, 500); // หน่วงนิดนึงเพื่อไม่ให้ยิงบ่อยเกิน

    // Cleanup ถ้ายังไม่ทันยิง request เก่า ให้ล้างก่อน
    return () => clearTimeout(timer);
  }, [query]);

  return (
    <div>
      <h2>🔍 ค้นหาผู้ใช้ (Real-time Search)</h2>
      <input
        type="text"
        value={query}
        onChange={(e) => setQuery(e.target.value)}
        placeholder="พิมพ์ชื่อผู้ใช้ เช่น Leanne"
      />

      {loading && <p>⏳ กำลังค้นหา...</p>}

      <ul>
        {results.length === 0 && !loading && query && <p>ไม่พบข้อมูล</p>}
        {results.map((user) => (
          <li key={user.id}>
            👤 {user.name} | ✉️ {user.email}
          </li>
        ))}
      </ul>
    </div>
  );
}

🔍 เทคนิคที่ใช้ในโค้ดนี้:
จุด	อธิบาย
query	state ที่เก็บคำค้น
useEffect(..., [query])	ดึงข้อมูลใหม่ทุกครั้งที่ query เปลี่ยน
setTimeout + clearTimeout	ทำ Debounce ป้องกันยิง API ทุกตัวอักษรที่พิมพ์
.filter()	กรองข้อมูลในฝั่ง client (หลังดึงจาก API)


✅ เคล็ดลับสอบ:
ถ้าโจทย์บอก “พิมพ์แล้วค้นหาอัตโนมัติแบบ realtime”
✅ ต้องใช้ useEffect
✅ ต้องดัก setTimeout + clearTimeout
✅ ใช้ .includes() สำหรับ search keyword
✅ คุม state ทั้ง query / loading / result


2 แนวหลักที่ใช้ในวงการจริง
🧠 1. Client-side Search (แบบที่เราทำเมื่อกี้)
ดึงข้อมูลมาทั้งหมดก่อน → แล้ว filter ใน React

เหมาะกับ:
ข้อมูลมีไม่มาก (เช่น < 1000 ชิ้น)
ไม่ต้องเรียก API ซ้ำบ่อย
โหลดทีเดียวจบ จัดการง่าย
✅ ข้อดี: เร็ว, ไม่ต้องพึ่ง backend
❌ ข้อเสีย: ถ้าข้อมูลเยอะจะโหลดนานและกิน RAM

🧠 2. Server-side Search (App Search ที่แท้ทรู)
ส่งคำค้นไปให้ Backend → Backend ส่งข้อมูลที่ตรงกับ keyword กลับมา

เช่น:
axios.get(`https://myapi.com/books?search=harry+potter`);

เหมาะกับ:
ข้อมูลเยอะมาก (เช่น คลังหนังสือ, ร้านค้า, คลังหนัง)
ต้องการ pagination, sorting, advanced filtering
ปรับ performance ได้จากฝั่ง backend
✅ ข้อดี: เร็วมาก (เฉพาะข้อมูลที่ตรง) ❌ ข้อเสีย: ต้องมี API รองรับการค้นหา (search endpoint)



🎯 ถ้าอยากทำแบบ App Search ที่เป็น Server-side จริง ๆ แนะนำโครงสร้างแบบนี้เลย:
const [query, setQuery] = useState("");
const [books, setBooks] = useState([]);

const searchBooks = async () => {
  const res = await axios.get(`/api/books?search=${query}`);
  setBooks(res.data);
};

พิมพ์เสร็จแล้ว "กดปุ่มค้นหา" → ไม่ต้อง fetch ตลอด
เหมาะกับระบบ Search App ที่มี ปุ่ม Search จริง ๆ


🔍 สรุป Requirement สั้น ๆ:
มีช่อง Input ให้ผู้ใช้พิมพ์ชื่อหนังสือที่ต้องการค้นหา
กดค้นหาแล้ว → ใช้ Google Books API
https://www.googleapis.com/books/v1/volumes?q=<keyword>
แสดงชื่อหนังสือทั้งหมดที่ได้จาก API เป็นรายการ List ด้านล่าง
✅ ตัวอย่างโค้ด React
import { useState } from "react";
import axios from "axios";

function BookSearchApp() {
  const [query, setQuery] = useState("");
  const [books, setBooks] = useState([]);
  const [loading, setLoading] = useState(false);

  const searchBooks = async () => {
    if (!query.trim()) return;

    setLoading(true);
    try {
      const res = await axios.get(
        `https://www.googleapis.com/books/v1/volumes?q=${encodeURIComponent(query)}`
      );
      const items = res.data.items || [];
      setBooks(items);
    } catch (err) {
      console.error("เกิดข้อผิดพลาดตอนดึงข้อมูลจ้า:", err);
    }
    setLoading(false);
  };

  const handleSubmit = (e) => {
    e.preventDefault();
    searchBooks();
  };

  return (
    <div style={{ padding: "20px" }}>
      <h2>📚 Find a Book</h2>
      <form onSubmit={handleSubmit}>
        <input
          type="text"
          value={query}
          onChange={(e) => setQuery(e.target.value)}
          placeholder="เช่น React JS"
        />
        <button type="submit">ค้นหา</button>
      </form>

      {loading && <p>⏳ กำลังโหลด...</p>}

      <ul>
        {books.map((book) => (
          <li key={book.id}>
            {book.volumeInfo.title}
          </li>
        ))}
      </ul>
    </div>
  );
}

export default BookSearchApp;



✅ โค้ด Real-time Search + Debounce ด้วย setTimeout
import { useEffect, useState } from "react";
import axios from "axios";

function BookSearchApp() {
  const [query, setQuery] = useState("");
  const [books, setBooks] = useState([]);
  const [loading, setLoading] = useState(false);

  useEffect(() => {
    if (!query.trim()) {
      setBooks([]);
      return;
    }

    setLoading(true);

    const delayDebounce = setTimeout(() => {
      axios
        .get(
          `https://www.googleapis.com/books/v1/volumes?q=${encodeURIComponent(
            query
          )}`
        )
        .then((res) => {
          const items = res.data.items || [];
          setBooks(items);
        })
        .catch((err) => {
          console.error("เกิดข้อผิดพลาดตอนค้นหาจ้า:", err);
        })
        .finally(() => {
          setLoading(false);
        });
    }, 600); // หน่วง 600ms (debounce)

    // เคลียร์ timeout ทุกครั้งที่ query เปลี่ยนก่อนครบเวลา
    return () => clearTimeout(delayDebounce);
  }, [query]);

  return (
    <div style={{ padding: "20px" }}>
      <h2>📚 Real-time Book Search</h2>
      <input
        type="text"
        value={query}
        onChange={(e) => setQuery(e.target.value)}
        placeholder="พิมพ์ชื่อหนังสือ เช่น React"
      />

      {loading && <p>⏳ กำลังค้นหา...</p>}

      <ul>
        {books.map((book) => (
          <li key={book.id}>
            {book.volumeInfo.title}
          </li>
        ))}
      </ul>
    </div>
  );
}

export default BookSearchApp;

🧠 อธิบายการ Debounce แบบบ้าน ๆ:
ทุกครั้งที่พิมพ์ → จะ รอ 600ms ก่อนยิง API
ถ้าระหว่างนั้นมีการพิมพ์เพิ่ม → จะเคลียร์ของเก่า แล้วเริ่มจับเวลาใหม่
ช่วยให้ ไม่ยิง API ถี่ ๆ ทุกตัวอักษร

✅ จุดที่สอบออกแน่นอน:
สิ่งที่ใช้	ทำไมสอบชอบออก
useEffect + query	รันเมื่อ query เปลี่ยน
setTimeout + clearTimeout	Debounce search
axios.get(...)	ดึงข้อมูลจาก API จริง
Loading State	UX ดี ไม่พัง





















































