---
topic: react
language: fa
version: 1.4
---

# سوالات مصاحبه React

## دسته‌بندی‌های موجود

- مبانی React
- JSX و رندرینگ
- کامپوننت‌ها
- Props و State
- Hooks
- Effects و چرخه حیات
- فرم‌ها و رویدادها
- Context API
- مدیریت State
- بهینه‌سازی عملکرد
- رفتار رندرینگ
- Concurrent React
- Server Components
- SSR / Hydration
- معماری و الگوها
- داخلی‌های React
- موارد- داخلیهای React
- موارد لبه و تلهها

## سطح دشواری

- آسان
- متوسط
- سخت

## 🧠 سوال 1

**شناسه**: react-001
**عنوان**: React چیست و چه مشکلی را حل می‌کند؟
**سطح دشواری**: آسان
**دسته‌بندی**: مبانی React

### پاسخ 📄

React یک کتابخانه جاوااسکریپت متن‌باز است که توسط Meta (فیسبوک) برای ساخت رابط‌های کاربری، عمدتاً اپلیکیشن‌های تک‌صفحه‌ای، توسعه یافته است.

این کتابخانه چندین چالش اصلی فرانت‌اند را حل می‌کند:

- **هماهنگ نگه داشتن UI با state** — در React، نمایش تابعی خالص از state است. هنگام تغییر state، React به‌طور خودکار بخش‌های مرتبط UI را دوباره رندر می‌کند.
- **به‌روزرسانی کارآمد DOM** — React از Virtual DOM استفاده می‌کند تا عملیات گران‌قیمت DOM واقعی را با محاسبه حداقل تغییرات لازم به حداقل برساند.
- **کامپوننت‌های UI قابل استفاده مجدد** — مدل کامپوننت به توسعه‌دهندگان اجازه می‌دهد UI‌های پیچیده را از قطعات کوچک، مجزا و قابل تست بسازند.

React عمداً تنها بر لایه نمایش تمرکز دارد. مسیریابی، دریافت داده، و مدیریت state توسط اکوسیستم اطراف آن (React Router، TanStack Query، Zustand، Redux و غیره) انجام می‌شود.

چون React یک کتابخانه است نه یک فریمورک، به راحتی در اپلیکیشن‌های موجود ادغام می‌شود و به تیم‌ها کنترل کامل بر تصمیمات معماری می‌دهد.

## 🧠 سوال 2

**شناسه**: react-002
**عنوان**: Virtual DOM چیست و React چگونه از آن استفاده می‌کند؟
**سطح دشواری**: آسان
**دسته‌بندی**: رفتار رندرینگ

### پاسخ 📄

Virtual DOM (VDOM) یک نمایش سبک‌وزن در حافظه از درخت DOM واقعی است. این یک درخت شیء جاوااسکریپت ساده است که ساختار UI را توصیف می‌کند.

هنگامی که state یا props یک کامپوننت تغییر می‌کند، React:

1. **رندر** — یک درخت Virtual DOM جدید با فراخوانی تابع رندر کامپوننت می‌سازد.
2. **مقایسه (Diff)** — درخت جدید را با درخت قبلی مقایسه می‌کند (تطبیق) تا تغییرات را پیدا کند.
3. **اعمال (Patch)** — فقط گره‌های تغییریافته را در DOM واقعی اعمال می‌کند (فاز commit).

این فرآیند **تطبیق (reconciliation)** نام دارد و تغییرات DOM را به حداقل می‌رساند، چون لمس کردن DOM واقعی بسیار گران‌تر از مقایسه اشیاء جاوااسکریپت است.

React در هر تغییر state کل صفحه را دوباره رندر نمی‌کند — فقط زیردرختی که به state تغییریافته وابسته است ارزیابی می‌شود.

```jsx
// هنگام تغییر count، React Counter را دوباره رندر می‌کند،
// حداقل به‌روزرسانی DOM را محاسبه کرده و فقط آن را اعمال می‌کند.
function Counter() {
  const [count, setCount] = React.useState(0);
  return <button onClick={() => setCount((c) => c + 1)}>{count}</button>;
}
```

**مهم:** VDOM یک جزئیات پیاده‌سازی است. React Native، برای مثال، از reconciler ری‌اکت بدون DOM مرورگر استفاده می‌کند.

## 🧠 سوال 3

**شناسه**: react-003
**عنوان**: JSX چیست و چگونه زیر پوسته کار می‌کند؟
**سطح دشواری**: آسان
**دسته‌بندی**: JSX و رندرینگ

### پاسخ 📄

JSX (JavaScript XML) یک افزونه نحوی است که به شما اجازه می‌دهد markup شبیه HTML را درون جاوااسکریپت بنویسید. این خودش جاوااسکریپت معتبر نیست — باید قبل از اجرا توسط یک transpiler (Babel یا کامپایلر TypeScript) کامپایل شود.

هر عنصر JSX به یک فراخوانی `React.createElement()` (runtime کلاسیک) یا یک فراخوانی `jsx()` از `react/jsx-runtime` (runtime خودکار، React 17+) تبدیل می‌شود:

```jsx
// JSX
const element = <h1 className="title">سلام، {name}</h1>;

// کامپایل‌شده (runtime خودکار — React 17+)
import { jsx as _jsx } from 'react/jsx-runtime';
const element = _jsx('h1', { className: 'title', children: `سلام، ${name}` });
```

نتیجه یک شیء جاوااسکریپت ساده است — یک **React element** (vnode):

```js
{
  type: 'h1',
  props: { className: 'title', children: 'سلام، علی' },
  key: null,
  ref: null,
}
```

**قوانین کلیدی JSX:**

- یک کامپوننت باید یک عنصر ریشه برگرداند (برای چندین ریشه از `<>...</>` fragments استفاده کنید).
- `class` به `className` تبدیل می‌شود؛ `for` به `htmlFor`.
- همه تگ‌ها باید بسته شوند: `<img />`, `<br />`.
- عبارات جاوااسکریپت داخل `{}` قرار می‌گیرند.
- نام کامپوننت‌ها باید با حرف بزرگ شروع شوند تا از تگ‌های HTML متمایز شوند.

## 🧠 سوال 4

**شناسه**: react-004
**عنوان**: کامپوننت‌های functional در React چیستند؟
**سطح دشواری**: آسان
**دسته‌بندی**: کامپوننت‌ها

### پاسخ 📄

یک کامپوننت functional یک تابع جاوااسکریپت است که یک شیء `props` دریافت می‌کند و JSX (عناصر React) برمی‌گرداند. این روش استاندارد نوشتن کامپوننت‌ها در React مدرن است.

```jsx
function Greeting({ name, role = 'user' }) {
  return (
    <div>
      <h1>سلام، {name}!</h1>
      <p>نقش: {role}</p>
    </div>
  );
}

// نحو arrow function — به همین اندازه معتبر است
const Greeting = ({ name, role = 'user' }) => (
  <div>
    <h1>سلام، {name}!</h1>
    <p>نقش: {role}</p>
  </div>
);
```

قبل از React 16.8، کامپوننت‌های functional "بدون state" بودند — state و چرخه حیات به کامپوننت‌های class نیاز داشتند. Hooks این را تغییر داد: کامپوننت‌های functional اکنون می‌توانند از state (`useState`)، side effects (`useEffect`)، context، refs و هر custom hook استفاده کنند.

**چرا کامپوننت‌های functional ترجیح داده می‌شوند:**

- مدل ذهنی ساده‌تر — بدون `this`، بدون قراردادهای نام‌گذاری متدهای چرخه حیات.
- آزمون‌پذیری آسان‌تر — توابع خالص قابل پیش‌بینی هستند.
- استنتاج بهتر TypeScript.
- تمام ویژگی‌های React (Concurrent Mode، Server Components) حول توابع طراحی شده‌اند.

کامپوننت‌های class هنوز کار می‌کنند اما دیگر رویکرد توصیه‌شده نیستند.

## 🧠 سوال 5

**شناسه**: react-005
**عنوان**: Props در React چیستند و چگونه کار می‌کنند؟
**سطح دشواری**: آسان
**دسته‌بندی**: Props و State

### پاسخ 📄

Props (مخفف "properties") مکانیزم انتقال داده از کامپوننت والد به کامپوننت فرزند هستند. آن‌ها فقط-خواندنی هستند — یک کامپوننت هرگز نباید props خودش را تغییر دهد.

```jsx
// والد داده را از طریق props منتقل می‌کند
function App() {
  return <UserCard name="علی" age={30} isAdmin={true} />;
}

// فرزند props را به عنوان یک شیء ساده دریافت می‌کند
function UserCard({ name, age, isAdmin }) {
  return (
    <div>
      <h2>{name}</h2>
      <p>سن: {age}</p>
      {isAdmin && <span>مدیر</span>}
    </div>
  );
}
```

**انواع Prop:**

- رشته‌ها: `name="علی"` (نیازی به آکولاد نیست)
- هر چیز دیگری (اعداد، booleans، آرایه‌ها، اشیاء، توابع): `age={30}`
- boolean حذف‌شده: `<Button disabled />` معادل `disabled={true}` است

**prop `children`** — محتوای بین تگ‌های باز و بسته به عنوان `props.children` منتقل می‌شود:

```jsx
function Card({ children, title }) {
  return (
    <div className="card">
      <h3>{title}</h3>
      {children}
    </div>
  );
}

// استفاده
<Card title="اطلاعات">
  <p>محتوا</p>
</Card>;
```

**پخش Props** — از عملگر spread برای ارسال همه props استفاده کنید:

```jsx
function Button({ className, ...rest }) {
  return <button className={`btn ${className}`} {...rest} />;
}
```

## 🧠 سوال 6

**شناسه**: react-006
**عنوان**: State در React چیست و چه تفاوتی با props دارد؟
**سطح دشواری**: آسان
**دسته‌بندی**: Props و State

### پاسخ 📄

State داده‌های قابل تغییر است که درون یک کامپوننت مدیریت می‌شود. هنگامی که state تغییر می‌کند، React کامپوننت را برای نشان دادن state جدید دوباره رندر می‌کند. برخلاف props (که متعلق به والد است)، state متعلق به خود کامپوننت است و توسط آن کنترل می‌شود.

```jsx
import { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0); // مقدار اولیه: 0

  return (
    <div>
      <p>تعداد: {count}</p>
      <button onClick={() => setCount((c) => c + 1)}>+</button>
      <button onClick={() => setCount((c) => c - 1)}>-</button>
    </div>
  );
}
```

**Props در مقابل State:**

|                        | Props                             | State                              |
| ---------------------- | --------------------------------- | ---------------------------------- |
| مالک                   | کامپوننت والد                     | خود کامپوننت                       |
| قابل تغییر؟            | خیر (فقط-خواندنی)                 | بله (از طریق setter)               |
| باعث re-render می‌شود؟ | بله (زمانی که والد re-render کند) | بله (زمانی که setter فراخوانی شود) |
| منتقل می‌شود از طریق   | آرگومان تابع                      | hook `useState`                    |

**فرم به‌روزرسانی functional** — هنگامی که مقدار جدید به مقدار قبلی وابسته است، یک تابع به setter منتقل کنید. این برای صحت در callback های async یا به‌روزرسانی‌های دسته‌ای ضروری است:

```js
setCount((prev) => prev + 1); // ایمن — همیشه آخرین مقدار را می‌خواند
setCount(count + 1); // ممکن است در concurrent mode قدیمی باشد
```

**State محلی و캡encapsulated است** — کامپوننت‌های همتا مستقیماً state را به اشتراک نمی‌گذارند. برای اشتراک‌گذاری state، آن را به نزدیک‌ترین جد مشترک انتقال دهید.

## 🧠 سوال 7

**شناسه**: react-007
**عنوان**: React چگونه رویدادها را مدیریت می‌کند؟
**سطح دشواری**: آسان
**دسته‌بندی**: فرم‌ها و رویدادها

### پاسخ 📄

React از یک **سیستم رویداد synthetic** استفاده می‌کند که رویدادهای بومی DOM مرورگر را در بر می‌گیرد. React یک event listener واحد را در ریشه درخت React نصب می‌کند (نه روی هر عنصر)، و رویدادها را از طریق event delegation به handler های صحیح ارسال می‌کند.

```jsx
function Form() {
  function handleSubmit(event) {
    event.preventDefault(); // مانند preventDefault بومی کار می‌کند
    console.log('ارسال شد');
  }

  function handleChange(event) {
    console.log(event.target.value); // SyntheticEvent — همان API بومی
  }

  return (
    <form onSubmit={handleSubmit}>
      <input onChange={handleChange} />
    </form>
  );
}
```

**تفاوت‌های کلیدی با رویدادهای DOM:**

- نام‌های event با camelCase نوشته می‌شوند: `onClick`، `onChange`، `onSubmit` (نه `onclick`).
- شما یک تابع منتقل می‌کنید، نه یک رشته: `onClick={handler}` نه `onclick="handler()"`.
- رویدادها bubble می‌کنند همانطور که انتظار می‌رود؛ از `event.stopPropagation()` برای متوقف کردن استفاده کنید. `event.persist()` در React 17+ ضروری نیست چون SyntheticEvents دیگر pooled نمی‌شوند.

**انتشار رویداد** همانند رویدادهای بومی (حباب‌ها، مرحله ضبط) عمل می‌کند. می‌توانید با `event.stopPropagation()` انتشار را متوقف کنید.

React 17 ریشه واگذاری رویداد را از `document` به کانتینر ریشه React تغییر داده است، که باعث می‌شود ترکیب میکرو-فرانت‌اند با نسخه‌های مختلف React ایمن‌تر شود.

## 🧠 سوال 8

**شناسه**: react-008
**عنوان**: رندرینگ شرطی در React چگونه کار می‌کند؟
**سطح دشواری**: آسان
**دسته‌بندی**: JSX و رندرینگ

### پاسخ 📄

React هیچ دستور ویژهای برای شرط ها ندارد — شما از عبارات جاوااسکریپت معمولی درون JSX استفاده میکنید.

**عملگر سهگانه (Ternary)** — رایج ترین الگو:

```jsx
function Alert({ type, message }) {
  return (
    <div className={`alert alert-${type}`}>
      {type === 'error' ? <ErrorIcon /> : <InfoIcon />}
      <span>{message}</span>
    </div>
  );
}
```

**اتصال کوتاه `&&`** — سمت راست را فقط زمانی رندر میکند که سمت چپ truthy باشد:

```jsx
{
  isLoggedIn && <Dashboard />;
}
```

**تله:** اگر سمت چپ `0` باشد، React عدد `0` را در DOM رندر میکند (چون `0` falsy است اما یک مقدار قابل رندر معتبر نیز هست). برای امنیت از `!!` یا ternary استفاده کنید:

```jsx
{
  items.length > 0 && <List items={items} />;
} // ایمن — boolean
{
  items.length && <List items={items} />;
} // خطرناک — اگر خالی باشد "0" رندر میکند
```

**الگوی بازگشت زودهنگام:**

```jsx
function Profile({ user }) {
  if (!user) return <p>Loading...</p>;
  return <div>{user.name}</div>;
}
```

**`null` برای رندر نکردن هیچ چیز:**

```jsx
function Banner({ visible, message }) {
  if (!visible) return null;
  return <div className="banner">{message}</div>;
}
```

## 🧠 سوال 9

**شناسه**: react-009
**عنوان**: چگونه لیست‌ها را در React رندر می‌کنید و `key` چرا مهم است؟
**سطح دشواری**: آسان
**دسته‌بندی**: JSX و رندرینگ

### پاسخ 📄

از `Array.map()` برای تبدیل آرایه‌های داده به عناصر React استفاده کنید. هر عنصر در یک لیست باید یک prop `key` منحصربه‌فرد داشته باشد:

```jsx
function TodoList({ todos }) {
  return (
    <ul>
      {todos.map((todo) => (
        <li key={todo.id}>
          <span>{todo.text}</span>
          {todo.done && <span>✓</span>}
        </li>
      ))}
    </ul>
  );
}
```

**چرا `key` مهم است:**

وقتی React یک لیست را تطبیق می‌دهد، از `key` برای تطبیق عناصر بین رندر قبلی و جدید استفاده می‌کند. بدون کلیدهای پایدار، React به تطبیق مبتنی بر شاخص بازمی‌گردد، که باعث می‌شود هنگام مرتب‌سازی مجدد، درج یا حذف موارد، رفتار نادرستی رخ دهد:

- حالت کامپوننت (مانند مقدار تایپ شده ورودی) به عنصر اشتباه متصل می‌شود.
- جهش‌های غیرضروری DOM رخ می‌دهد.
- انیمیشن‌ها و فوکوس مختل می‌شوند.

**قوانین مربوط به کلیدها:**

- باید در بین سایر موارد منحصر به فرد باشد\*\* (نه منحصر به فرد سراسری).
- باید پایدار باشد\*\* - یک آیتم باید در رندرهای مختلف، کلید یکسانی داشته باشد.
- باید یک شناسه پایدار از داده‌های شما باشد (شناسه پایگاه داده، UUID). از استفاده از اندیس آرایه خودداری کنید، مگر اینکه لیست ایستا باشد و هرگز تغییر ترتیب ندهد.

```jsx
// بد — index ناپایدار است هنگام مرتب‌سازی/فیلتر کردن
{
  items.map((item, i) => <Item key={i} {...item} />);
}

// خوب — ID های ثابت
{
  items.map((item) => <Item key={item.id} {...item} />);
}
```

## 🧠 سوال 10

**شناسه**: react-010
**عنوان**: کامپوننت‌های controlled در مقابل uncontrolled چیستند؟
**سطح دشواری**: آسان
**دسته‌بندی**: فرم‌ها و رویدادها

### پاسخ 📄

**Controlled components** مقدار فرم خود را از React state دریافت می‌کنند. React "منبع حقیقت" است:

```jsx
function ControlledInput() {
  const [value, setValue] = useState('');

  return (
    <input
      value={value} // React مقدار را کنترل می‌کند
      onChange={(e) => setValue(e.target.value)}
    />
  );
}
```

**Uncontrolled components** مقدار خود را در DOM ذخیره می‌کنند. شما با یک `ref` هنگام نیاز به آن، مقدار را می‌خوانید:

```jsx
function UncontrolledInput() {
  const inputRef = useRef(null);

  function handleSubmit() {
    console.log(inputRef.current.value); //بنا به تقاضا بخوانید
  }

  return (
    <>
      <input ref={inputRef} defaultValue="پیش‌فرض" />
      <button onClick={handleSubmit}>ارسال</button>
    </>
  );
}
```

|                                          | Controlled                    | Uncontrolled               |
| ---------------------------------------- | ----------------------------- | -------------------------- |
| اعتبارسنجی در هر keystroke               | ✅ طبیعی                      | ❌ نیاز به polling با ref  |
| بازخورد فوری (فرمت، غیرفعال کردن submit) | ✅                            | ❌                         |
| ورودیهای فایل                            | ❌ نمیتوان مقدار را کنترل کرد | ✅ باید از ref استفاده شود |
| فرمهای ساده، یکپارچهسازیهای شخص ثالث     | ❌ کد بیشتر                   | ✅ کد کمتر                 |

اکثر فرم های React از کامپوننت های controlled استفاده میکنند. کتابخانه هایی مانند React Hook Form رویکرد ترکیبی دارند (uncontrolled در زیرساخت برای عملکرد، API شبیه controlled برای اعتبارسنجی).
ا منطق وابسته به مقادیر.

## 🧠 سوال 11

**شناسه**: react-011
**عنوان**: React Fragment چیست و چه زمانی باید از آن استفاده کنید؟
**سطح دشواری**: آسان
**دسته‌بندی**: JSX و رندرینگ

### پاسخ 📄

Fragment به یک کامپوننت اجازه می‌دهد چندین عنصر را بدون اضافه کردن یک نود DOM اضافی به عنوان wrapper برگرداند.

```jsx
// بدون Fragment — یک <div> غیرضروری اضافه می‌شود
function Columns() {
  return (
    <div>
      <td>Name</td>
      <td>Age</td>
    </div>
  ); // HTML نامعتبر — <div> داخل <tr>
}

// با Fragment — بدون نود DOM اضافه
function Columns() {
  return (
    <>
      <td>Name</td>
      <td>Age</td>
    </>
  );
}
```

**دو نحو برای آن وجود دارد:**

```jsx
// کوتاه‌نویسی — نمی‌تواند props بگیرد
<>...</>;

// صریح — وقتی به key نیاز دارید لازم است (مثلا در map روی یک لیست)
function List({ items }) {
  return items.map((item) => (
    <React.Fragment key={item.id}>
      <dt>{item.term}</dt>
      <dd>{item.description}</dd>
    </React.Fragment>
  ));
}
```

**موارد استفاده:**

- برگرداندن چندین سلول جدول (`<td>`) یا سطر (`<tr>`) از یک کامپوننت
- گروه‌بندی عناصری که از یک کامپوننت برمی‌گردند بدون شلوغ کردن DOM
- رندر کردن لیستی که هر آیتم آن چندین عنصر هم‌سطح تولید می‌کند

Fragment ها هیچ خروجی‌ای در DOM تولید نمی‌کنند، بنابراین روی استایل یا layout اثری ندارند.

## 🧠 سوال 12

**شناسه**: react-012
**عنوان**: تفاوت بین class component و functional component چیست؟
**سطح دشواری**: آسان
**دسته‌بندی**: کامپوننت‌ها

### پاسخ 📄

هر دو نوع می‌توانند خروجی یکسانی تولید کنند، اما از نظر syntax، API، و نحوه مدیریت state و lifecycle تفاوت‌های مهمی دارند.

**Class component ها** از کلاس‌های ES6 استفاده می‌کنند، `this` دارند، متدهای lifecycle دارند و از `this.state` استفاده می‌کنند:

```jsx
class Counter extends React.Component {
  state = { count: 0 };

  componentDidMount() {
    document.title = `Count: ${this.state.count}`;
  }

  componentDidUpdate() {
    document.title = `Count: ${this.state.count}`;
  }

  render() {
    return (
      <button onClick={() => this.setState((s) => ({ count: s.count + 1 }))}>
        {this.state.count}
      </button>
    );
  }
}
```

**Functional component ها** از hook ها استفاده می‌کنند:

```jsx
function Counter() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    document.title = `Count: ${count}`;
  });

  return <button onClick={() => setCount((c) => c + 1)}>{count}</button>;
}
```

**تفاوت‌های کلیدی:**

|                       | Class Components               | Functional Components              |
| --------------------- | ------------------------------ | ---------------------------------- |
| State                 | `this.state` + `this.setState` | `useState`                         |
| Lifecycle             | `componentDidMount` و غیره     | `useEffect`                        |
| اتصال `this`          | لازم است                       | لازم نیست                          |
| استفاده مجدد از کد    | Mixins (مشکل‌دار)              | Custom hooks (تمیزتر)              |
| Error boundary        | پشتیبانی می‌شود                | هنوز نه (تا React 18)              |
| ویژگی‌های آینده React | در اولویت نیست                 | همه قابلیت‌های جدید برای توابع‌اند |

Class component ها کاملا پشتیبانی می‌شوند، اما legacy محسوب می‌شوند. تمام API های جدید React مثل Concurrent Mode و Server Components حول توابع طراحی شده‌اند.

## 🧠 سوال 13

**شناسه**: react-013
**عنوان**: Reconciliation در React چیست؟
**سطح دشواری**: متوسط
**دسته‌بندی**: رفتار رندرینگ

### پاسخ 📄

Reconciliation فرایندی است که React با آن تشخیص می‌دهد بین دو رندر چه چیزی در UI تغییر کرده و DOM را بر همان اساس به‌روزرسانی می‌کند.

وقتی state یا props تغییر می‌کند، React تابع render کامپوننت را اجرا می‌کند و یک درخت virtual DOM جدید می‌سازد. سپس این درخت جدید را با درخت قبلی **diff** می‌کند. این کار با یک الگوریتم heuristic انجام می‌شود که دو فرض مهم دارد:

1. **نوع‌های متفاوت عنصر، درخت‌های متفاوتی تولید می‌کنند.** اگر نوع ریشه عوض شود (مثلا `<div>` به `<span>`)، React کل زیر‌درخت قدیمی را حذف می‌کند و یکی جدید از صفر می‌سازد؛ یعنی همه child component ها هم unmount می‌شوند.

2. **`key` عناصر پایدار را بین رندرها مشخص می‌کند.** هنگام diff کردن لیست‌ها، React از prop `key` استفاده می‌کند تا عناصر را بین دو رندر match کند. عناصری با key یکسان، همان عنصر در نظر گرفته می‌شوند و درجا update می‌شوند؛ key های حذف‌شده یا جدید باعث unmount/mount می‌شوند.

```jsx
// React فرض می‌کند عنصر ریشه عوض شده — Foo را unmount و Bar را mount می‌کند
{
  condition ? <Foo /> : <Bar />;
}

// React همان نوع ریشه را می‌بیند — فقط props های Foo را update می‌کند
{
  condition ? <Foo color="red" /> : <Foo color="blue" />;
}
```

**چرا برای performance مهم است:** reconciler ری‌اکت با استفاده از این heuristic ها از مقایسه‌های گران‌قیمت کل درخت جلوگیری می‌کند. نتیجه، diff کردن درخت با پیچیدگی `O(n)` است، نه الگوریتم naive با پیچیدگی `O(n^3)`.

Reconciler از renderer جدا است. React DOM، React Native و React Three Fiber همگی از یک reconciler مشترک استفاده می‌کنند، اما خروجی‌شان برای محیط‌های متفاوتی است.

## 🧠 سوال 14

**شناسه**: react-014
**عنوان**: Prop drilling چیست و چگونه آن را حل می‌کنید؟
**سطح دشواری**: آسان
**دسته‌بندی**: Props و State

### پاسخ 📄

Prop drilling زمانی رخ می‌دهد که داده باید از چندین لایه از کامپوننت‌های میانی عبور کند، در حالی که آن کامپوننت‌های میانی خودشان به آن داده نیاز ندارند و فقط آن را به پایین‌تر پاس می‌دهند.

```jsx
// Prop drilling — theme باید از App → Layout → Sidebar → Button عبور کند
function App() {
  const [theme, setTheme] = useState('dark');
  return <Layout theme={theme} setTheme={setTheme} />;
}
function Layout({ theme, setTheme }) {
  return <Sidebar theme={theme} setTheme={setTheme} />;
}
function Sidebar({ theme, setTheme }) {
  return <ThemeButton theme={theme} setTheme={setTheme} />;
}
function ThemeButton({ theme, setTheme }) {
  return (
    <button onClick={() => setTheme((t) => (t === 'dark' ? 'light' : 'dark'))}>
      {theme}
    </button>
  );
}
```

**مشکلاتی که ایجاد می‌کند:**

- کامپوننت‌های میانی به داده‌ای که استفاده نمی‌کنند وابسته می‌شوند
- refactor کردن سخت می‌شود، چون اضافه شدن یک prop نیاز به تغییر همه لایه‌ها دارد
- استفاده مجدد از کامپوننت‌ها به‌صورت مستقل سخت‌تر می‌شود

**راه‌حل‌ها:**

1. **Context API** — داده را در یک سطح بالا provide کنید و هرجا در درخت لازم بود consume کنید، بدون اینکه مجبور به پاس دادن آن از همه لایه‌ها باشید:

```jsx
const ThemeContext = createContext('light');
// درخت را wrap کنید: <ThemeContext.Provider value={theme}>
// هرجا لازم بود بخوانید: const theme = useContext(ThemeContext);
```

2. **کتابخانه‌های مدیریت state** مثل Zustand، Redux و Jotai — یک store سراسری که از هر کامپوننتی قابل دسترسی است

3. **Component composition** — به‌جای drill کردن داده، کامپوننت‌ها را به‌صورت children یا props پاس بدهید:

```jsx
function Layout({ children }) {
  return <div>{children}</div>;
}
// والد مشخص می‌کند داخل Layout چه چیزی قرار بگیرد، پس drilling لازم نیست
```

## 🧠 سوال 15

**شناسه**: react-015
**عنوان**: کامپوننت `StrictMode` چیست و چه کاری انجام می‌دهد؟
**سطح دشواری**: متوسط
**دسته‌بندی**: مبانی React

### پاسخ 📄

`<React.StrictMode>` یک wrapper مخصوص محیط توسعه است که warning ها و رفتارهای اضافی را فعال می‌کند تا به شما کمک کند مشکلات احتمالی اپلیکیشن را پیدا کنید.

```jsx
import { StrictMode } from 'react';
import { createRoot } from 'react-dom/client';

createRoot(document.getElementById('root')).render(
  <StrictMode>
    <App />
  </StrictMode>,
);
```

**StrictMode چه کارهایی انجام می‌دهد** (فقط در development و بدون اثر در production):

1. **تابع‌های render، مقداردهی اولیه state، و reducer ها را دوبار اجرا می‌کند** — تا side effect هایی را پیدا کند که در توابع supposedly pure نباید وجود داشته باشند. مثلا اگر داخل render به‌اشتباه یک شمارنده را زیاد کنید، این مشکل آشکار می‌شود.

2. **هر کامپوننت را یک‌بار mount → unmount → remount می‌کند** (در React 18+) — تا بررسی کند effect ها cleanup درست دارند. این رفتار شبیه‌سازی می‌کند که اگر یک کامپوننت حفظ و دوباره بازیابی شود چه اتفاقی می‌افتد.

3. **درباره API های deprecated هشدار می‌دهد** — مثل lifecycle های قدیمی (`componentWillMount` و غیره)، string ref های قدیمی، `findDOMNode` و موارد مشابه

4. **mutation ناخواسته state را آشکار می‌کند** — و کمک می‌کند باگ‌هایی که از تغییر مستقیم state به وجود می‌آیند دیده شوند

StrictMode فقط روی زیر‌درختی اعمال می‌شود که آن را wrap کرده است، بنابراین می‌توانید آن را برای بخش‌های خاصی از اپلیکیشن به‌صورت انتخابی فعال کنید.

## 🧠 سوال 16

**شناسه**: react-016
**عنوان**: `React.memo` چیست و چه زمانی کمک می‌کند؟
**سطح دشواری**: متوسط
**دسته‌بندی**: بهینه‌سازی عملکرد

### پاسخ 📄

`React.memo` یک higher-order component است که خروجی رندر یک functional component را memoize می‌کند. اگر props کامپوننت تغییر نکرده باشد (با shallow equality)، React از re-render شدن آن رد می‌شود و از خروجی قبلی استفاده می‌کند.

```jsx
const UserCard = React.memo(function UserCard({ name, age }) {
  console.log('rendering UserCard');
  return (
    <div>
      {name} — {age}
    </div>
  );
});

// اگر parent دوباره رندر شود اما name و age تغییر نکرده باشند،
// UserCard دوباره رندر نمی‌شود.
```

**چه زمانی کمک می‌کند:**

- وقتی parent زیاد re-render می‌شود ولی child از آن state پرنوسان استفاده نمی‌کند
- وقتی خود کامپوننت رندر گرانی دارد، مثلا محاسبات پیچیده یا child node های زیاد
- وقتی props پایدار هستند، مثل primitive ها یا object/function هایی که memoize شده‌اند

**چه زمانی کمک نمی‌کند یا حتی ضرر دارد:**

- وقتی props در هر رندر تغییر می‌کنند و shallow comparison فقط سربار اضافه می‌آورد
- وقتی props شامل object یا function هایی هستند که در parent به‌صورت inline ساخته می‌شوند و هر بار reference جدید دارند

```jsx
// این memo را بی‌اثر می‌کند — در هر رندر parent یک reference جدید می‌سازد
<UserCard style={{ color: 'red' }} onClick={() => doSomething()} />;

// راه‌حل: object و function را در parent memoize کنید
const style = useMemo(() => ({ color: 'red' }), []);
const handleClick = useCallback(() => doSomething(), []);
<UserCard style={style} onClick={handleClick} />;
```

**مقایسه سفارشی** — می‌توانید برای کنترل دقیق‌تر آرگومان دوم را هم بدهید:

```jsx
React.memo(MyComponent, (prevProps, nextProps) => {
  return prevProps.id === nextProps.id; // true = رد شدن از re-render
});
```

## 🧠 سوال 17

**شناسه**: react-017
**عنوان**: hook `useEffect` چیست و dependency array چگونه کار می‌کند؟
**سطح دشواری**: متوسط
**دسته‌بندی**: Effects و چرخه حیات

### پاسخ 📄

`useEffect` به شما اجازه می‌دهد یک کامپوننت را بعد از commit شدن رندر به DOM، با یک سیستم خارجی هماهنگ کنید؛ مثل DOM API، درخواست شبکه، subscription یا timer.

```jsx
useEffect(() => {
  // Side effect — به‌صورت پیش‌فرض بعد از هر رندر اجرا می‌شود
  document.title = `You clicked ${count} times`;
});
```

**Dependency array تعیین می‌کند effect چه زمانی اجرا شود:**

```jsx
// بدون dependency array — بعد از هر رندر اجرا می‌شود
useEffect(() => { ... });

// آرایه خالی — فقط یک‌بار بعد از mount اولیه اجرا می‌شود
useEffect(() => { ... }, []);

// با dependency — بعد از mount و هر بار که userId تغییر کند اجرا می‌شود
useEffect(() => {
  fetchUser(userId);
}, [userId]);
```

**تابع cleanup** — از effect برگردانده می‌شود. قبل از اجرای دوباره effect و همچنین هنگام unmount شدن کامپوننت اجرا می‌شود:

```jsx
useEffect(() => {
  const subscription = subscribe(userId, onMessage);
  return () => subscription.unsubscribe(); // cleanup
}, [userId]);
```

**React 18 + StrictMode** — در محیط توسعه، effect ها یک‌بار mount، cleanup و دوباره mount می‌شوند تا باگ‌های مربوط به cleanup آشکار شوند. این رفتار عمدی است.

**قواعد مهم:**

- هرگز `useEffect` را شرطی صدا نزنید؛ hook ها باید در همه رندرها با همان ترتیب فراخوانی شوند
- تمام مقادیری را که داخل effect خوانده می‌شوند در dependency array بگذارید؛ قانون `react-hooks/exhaustive-deps` در ESLint این را enforce می‌کند
- از `useEffect` برای event handler ها استفاده نکنید؛ handler ها باید مستقیم روی element قرار بگیرند

## 🧠 سوال 18

**شناسه**: react-018
**عنوان**: `useState` چیست و به‌روزرسانی state چگونه کار می‌کند؟
**سطح دشواری**: آسان
**دسته‌بندی**: Hooks

### پاسخ 📄

`useState` پایه‌ای‌ترین hook برای اضافه کردن state محلی به یک functional component است. این hook یک جفت مقدار برمی‌گرداند: مقدار فعلی state و یک تابع setter.

```jsx
const [state, setState] = useState(initialValue);
```

**به‌روزرسانی‌های state async و batched هستند** — صدا زدن `setState` بلافاصله مقدار `state` را عوض نمی‌کند. React یک re-render را زمان‌بندی می‌کند و همه به‌روزرسانی‌های state در همان event handler را در یک batch اعمال می‌کند:

```jsx
function handleClick() {
  setCount((c) => c + 1);
  setCount((c) => c + 1);
  // React آن‌ها را batch می‌کند — count بعد از یک re-render به اندازه 2 زیاد می‌شود
}
```

**فرم functional update** — وقتی مقدار جدید به مقدار قبلی وابسته است، یک تابع به setter بدهید:

```jsx
setState((prev) => ({ ...prev, name: 'Alice' }));
```

هر زمان داخل callback های async، `useEffect` یا event handler هایی هستید که ممکن است مقدار state در آن‌ها stale شده باشد، از این فرم استفاده کنید.

**مقداردهی اولیه state** — برای محاسبات گران، یک تابع پاس بدهید تا در هر رندر دوباره اجرا نشود:

```jsx
// بد — expensiveCalc() در هر رندر اجرا می‌شود، با اینکه فقط بار اول لازم است
const [value, setValue] = useState(expensiveCalc());

// خوب — فقط یک‌بار هنگام mount اولیه اجرا می‌شود
const [value, setValue] = useState(() => expensiveCalc());
```

**Object و array ها** — React state شیء را به‌صورت خودکار merge نمی‌کند (برخلاف `this.setState` در class component ها). باید خودتان spread کنید:

```jsx
setState((prev) => ({ ...prev, age: 31 })); // درست
setState({ age: 31 }); // غلط — بقیه فیلدها را حذف می‌کند
```

## 🧠 سوال 19

**شناسه**: react-019
**عنوان**: `useRef` چیست و چه زمانی باید از آن استفاده کنید؟
**سطح دشواری**: متوسط
**دسته‌بندی**: Hooks

### پاسخ 📄

`useRef` یک شیء `ref` قابل تغییر با property به نام `.current` برمی‌گرداند که بین رندرها حفظ می‌شود و با تغییرش re-render ایجاد نمی‌شود. این hook دو کاربرد اصلی دارد.

**1. دسترسی مستقیم به عناصر DOM:**

```jsx
function AutoFocusInput() {
  const inputRef = useRef(null);

  useEffect(() => {
    inputRef.current.focus();
  }, []);

  return <input ref={inputRef} />;
}
```

**2. نگه‌داری مقادیر mutable که نباید باعث re-render شوند:**

```jsx
function Timer() {
  const intervalId = useRef(null);
  const [seconds, setSeconds] = useState(0);

  function start() {
    intervalId.current = setInterval(() => {
      setSeconds((s) => s + 1);
    }, 1000);
  }

  function stop() {
    clearInterval(intervalId.current);
  }

  return (
    <>
      <p>{seconds}s</p>
      <button onClick={start}>Start</button>
      <button onClick={stop}>Stop</button>
    </>
  );
}
```

**ویژگی‌های مهم:**

- تغییر `ref.current` باعث re-render نمی‌شود، برخلاف `useState`
- شیء ref در تمام رندرها همان شیء قبلی باقی می‌ماند
- برای نگه داشتن previous value، شناسه animation frame، نمونه WebSocket، یا context های canvas مفید است

**مقایسه `useRef` و `useState`:**

|                              | `useRef`                  | `useState`        |
| ---------------------------- | ------------------------- | ----------------- |
| باعث re-render می‌شود؟       | خیر                       | بله               |
| مقدار بین رندرها حفظ می‌شود؟ | بله                       | بله               |
| نحوه دسترسی                  | `.current`                | مستقیم            |
| کاربرد اصلی                  | دسترسی DOM، ذخیره mutable | state رابط کاربری |

## 🧠 سوال 20

**شناسه**: react-020
**عنوان**: `useMemo` چیست و چه زمانی باید از آن استفاده کنید؟
**سطح دشواری**: متوسط
**دسته‌بندی**: بهینه‌سازی عملکرد

### پاسخ 📄

`useMemo` نتیجه یک محاسبه گران را memoize می‌کند و فقط زمانی آن را دوباره محاسبه می‌کند که یکی از dependency ها تغییر کرده باشد.

```jsx
const expensiveValue = useMemo(() => {
  return computeExpensiveValue(a, b);
}, [a, b]);
```

در re-render هایی که `a` و `b` تغییری نکرده‌اند، React محاسبه را رد می‌کند و نتیجه cache شده را برمی‌گرداند.

**چه زمانی از `useMemo` استفاده کنیم:**

1. **محاسبات گران** — مثل sort، filter یا transform کردن مجموعه داده‌های بزرگ:

```jsx
const sortedUsers = useMemo(
  () => [...users].sort((a, b) => a.name.localeCompare(b.name)),
  [users],
);
```

2. **پایدار نگه داشتن reference شیء یا آرایه** برای child component هایی که با `React.memo` پوشانده شده‌اند یا برای dependency array های `useEffect`:

```jsx
const config = useMemo(() => ({ theme, locale }), [theme, locale]);
// reference مربوط به config پایدار می‌ماند و effect یا memo check را بی‌دلیل دوباره فعال نمی‌کند
```

**چه زمانی نباید از `useMemo` استفاده کرد:**

- برای محاسبات ارزان، چون سربار memoization ممکن است از سودش بیشتر شود
- وقتی dependency ها در هر رندر عوض می‌شوند و cache عملا هیچ‌وقت استفاده نمی‌شود
- به‌عنوان بهینه‌سازی زودهنگام؛ اول profile بگیرید

**تفاوت `useMemo` و `useCallback`:**

```jsx
useMemo(() => fn(), [deps]); // مقدار برگشتی fn را memoize می‌کند
useCallback(fn, [deps]); // خود تابع fn را memoize می‌کند
```

React ممکن است تصمیم بگیرد مقدار cache شده `useMemo` را کنار بگذارد، مثلا تحت فشار حافظه. بنابراین برای درست کار کردن برنامه روی `useMemo` تکیه نکنید؛ فقط برای performance از آن استفاده کنید.

## 🧠 سوال 21

**شناسه**: react-021
**عنوان**: `useCallback` چیست و چه زمانی باید از آن استفاده کنید؟
**سطح دشواری**: متوسط
**دسته‌بندی**: بهینه‌سازی عملکرد

### پاسخ 📄

`useCallback` یک نسخه memoized از یک تابع callback برمی‌گرداند. تا زمانی که dependency های آن تغییر نکنند، هویت تابع بین رندرها حفظ می‌شود.

```jsx
const handleClick = useCallback(() => {
  doSomething(id);
}, [id]);
```

بدون `useCallback`، در هر رندر یک reference جدید از تابع ساخته می‌شود. این موضوع وقتی دردسرساز می‌شود که تابع را به این موارد پاس دهید:

- child component هایی که با `React.memo` پوشانده شده‌اند، چون shallow comparison را خراب می‌کند
- dependency array های `useEffect`، چون effect را بی‌دلیل دوباره اجرا می‌کند

**مثال عملی:**

```jsx
const MemoizedChild = React.memo(function Child({ onAction }) {
  console.log('Child rendered');
  return <button onClick={onAction}>Action</button>;
});

function Parent() {
  const [count, setCount] = useState(0);

  // بدون useCallback: در هر رندر یک تابع جدید ساخته می‌شود و Child همیشه re-render می‌شود
  const handleAction = useCallback(() => {
    console.log('action');
  }, []); // reference پایدار — Child فقط یک‌بار رندر می‌شود

  return (
    <>
      <button onClick={() => setCount((c) => c + 1)}>Count: {count}</button>
      <MemoizedChild onAction={handleAction} />
    </>
  );
}
```

**`useCallback(fn, deps)` معادل `useMemo(() => fn, deps)` است.**

**چه زمانی نباید از آن استفاده کرد:**

- وقتی child با `React.memo` پوشانده نشده و سودی ندارد
- وقتی تابع به چیزی پاس داده نمی‌شود که به referential stability وابسته باشد
- به‌عنوان بهینه‌سازی زودهنگام؛ قبل از استفاده profile بگیرید

## 🧠 سوال 22

**شناسه**: react-022
**عنوان**: قوانین hook ها چیست؟
**سطح دشواری**: متوسط
**دسته‌بندی**: Hooks

### پاسخ 📄

React برای اینکه hook ها درست کار کنند، دو قانون اصلی را enforce می‌کند.

**قانون 1: hook ها را فقط در بالاترین سطح صدا بزنید.**

هیچ‌وقت hook را داخل شرط، حلقه یا تابع تو‌در‌تو صدا نزنید. React برای اینکه هر hook را به state درست خودش وصل کند، به یکسان بودن ترتیب فراخوانی hook ها در همه رندرها وابسته است.

```jsx
// ❌ اشتباه — hook داخل شرط
function Component({ isLoggedIn }) {
  if (isLoggedIn) {
    const [user, setUser] = useState(null); // ترتیب hook ها را به‌هم می‌زند
  }
}

// ✅ درست — شرط را در نحوه استفاده از hook اعمال کنید
function Component({ isLoggedIn }) {
  const [user, setUser] = useState(null);
  if (!isLoggedIn) return null;
  // use user...
}
```

**قانون 2: hook ها را فقط از داخل توابع React صدا بزنید.**

hook ها باید فقط از اینجاها صدا زده شوند:

- functional component ها
- custom hook ها

هیچ‌وقت آن‌ها را از توابع معمولی جاوااسکریپت، class component ها یا مستقیم داخل event handler ها صدا نزنید.

**چرا این قوانین وجود دارند:**

React در داخل برای هر کامپوننت یک لیست از state های مربوط به hook ها را بر اساس ترتیب فراخوانی نگه می‌دارد. اگر یک hook شرطی صدا زده شود، ترتیب بین رندرها تغییر می‌کند و React state اشتباه را می‌خواند؛ نتیجه، باگ‌هایی است که پیدا کردنشان سخت است.

پکیج `eslint-plugin-react-hooks` هر دو قانون را به‌صورت خودکار در زمان توسعه بررسی می‌کند.

## 🧠 سوال 23

**شناسه**: react-023
**عنوان**: custom hook ها چیستند و چگونه آن‌ها را می‌نویسید؟
**سطح دشواری**: متوسط
**دسته‌بندی**: Hooks

### پاسخ 📄

یک custom hook یک تابع جاوااسکریپت است که نامش با `use` شروع می‌شود و می‌تواند hook های دیگر را صدا بزند. custom hook ها مهم‌ترین راه برای استخراج و اشتراک‌گذاری منطق stateful بین کامپوننت‌ها هستند و برای این کار جایگزین mixin ها و render prop ها شده‌اند.

```jsx
// useLocalStorage — state را در localStorage نگه می‌دارد
function useLocalStorage(key, initialValue) {
  const [storedValue, setStoredValue] = useState(() => {
    try {
      const item = window.localStorage.getItem(key);
      return item ? JSON.parse(item) : initialValue;
    } catch {
      return initialValue;
    }
  });

  const setValue = useCallback(
    (value) => {
      try {
        const valueToStore =
          value instanceof Function ? value(storedValue) : value;
        setStoredValue(valueToStore);
        window.localStorage.setItem(key, JSON.stringify(valueToStore));
      } catch (error) {
        console.error(error);
      }
    },
    [key, storedValue],
  );

  return [storedValue, setValue];
}

// استفاده — API آن شبیه useState است
function App() {
  const [theme, setTheme] = useLocalStorage('theme', 'light');
  return (
    <button onClick={() => setTheme((t) => (t === 'light' ? 'dark' : 'light'))}>
      {theme}
    </button>
  );
}
```

**بهترین روش‌ها:**

- همیشه نام آن را با `use` شروع کنید تا قوانین ESLint مربوط به hook ها بتوانند آن را درست بررسی کنند
- مقداری برگردانید که با الگوی hook ای که دور آن wrapper ساخته‌اید هماهنگ باشد، مثل tuple به شکل `[value, setter]` یا یک object
- هر custom hook باید فقط یک مسئولیت مشخص و متمرکز داشته باشد
- ورودی‌ها را به‌صورت آرگومان بگیرید و آن‌ها را hardcode نکنید تا hook قابل استفاده مجدد بماند
- منطق hook را مستقل از رندر نگه دارید و داخل hook JSX ننویسید

## 🧠 سوال 24

**شناسه**: react-024
**عنوان**: Context API چیست و چگونه از آن استفاده می‌کنید؟
**سطح دشواری**: متوسط
**دسته‌بندی**: Context API

### پاسخ 📄

Context API راهی برای پاس دادن داده در درخت کامپوننت‌ها بدون prop drilling فراهم می‌کند. Context شبیه یک "کانال پخش" است که هر descendant می‌تواند در آن subscribe کند.

**ساخت و provide کردن context:**

```jsx
import { createContext, useContext, useState } from 'react';

const ThemeContext = createContext('light'); // 'light' مقدار پیش‌فرض است

function ThemeProvider({ children }) {
  const [theme, setTheme] = useState('light');

  return (
    <ThemeContext.Provider value={{ theme, setTheme }}>
      {children}
    </ThemeContext.Provider>
  );
}
```

**مصرف context با `useContext`:**

```jsx
function ThemeButton() {
  const { theme, setTheme } = useContext(ThemeContext);

  return (
    <button onClick={() => setTheme((t) => (t === 'light' ? 'dark' : 'light'))}>
      Current: {theme}
    </button>
  );
}

// در اپلیکیشن
function App() {
  return (
    <ThemeProvider>
      <ThemeButton />
    </ThemeProvider>
  );
}
```

**نکته performance** — هر consumer یک context، وقتی value آن context تغییر کند دوباره رندر می‌شود. اگر value یک object باشد که inline ساخته شده، در هر رندر provider عوض می‌شود:

```jsx
// بد — در هر رندر یک object جدید ساخته می‌شود و همه consumer ها re-render می‌شوند
<Context.Provider value={{ theme, setTheme }}>

// بهتر — value را memoize کنید
const value = useMemo(() => ({ theme, setTheme }), [theme]);
<Context.Provider value={value}>
```

برای اپلیکیشن‌های بزرگ با state پرتغییر، برای داده‌های حساس به performance معمولا کتابخانه‌های مدیریت state انتخاب بهتری نسبت به Context هستند.

## 🧠 سوال 25

**شناسه**: react-025
**عنوان**: `useReducer` چیست و چه زمانی باید به‌جای `useState` از آن استفاده کنید؟
**سطح دشواری**: متوسط
**دسته‌بندی**: Hooks

### پاسخ 📄

`useReducer` یک جایگزین برای `useState` در مدیریت منطق state پیچیده است. این hook از الگوی Redux الهام گرفته است: یک reducer تابعی، state فعلی و یک action را می‌گیرد و state بعدی را برمی‌گرداند.

```jsx
import { useReducer } from 'react';

const initialState = { count: 0, step: 1 };

function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return { ...state, count: state.count + state.step };
    case 'decrement':
      return { ...state, count: state.count - state.step };
    case 'setStep':
      return { ...state, step: action.payload };
    case 'reset':
      return initialState;
    default:
      throw new Error(`Unknown action: ${action.type}`);
  }
}

function Counter() {
  const [state, dispatch] = useReducer(reducer, initialState);

  return (
    <div>
      <p>
        Count: {state.count} (step: {state.step})
      </p>
      <button onClick={() => dispatch({ type: 'increment' })}>+</button>
      <button onClick={() => dispatch({ type: 'decrement' })}>-</button>
      <button onClick={() => dispatch({ type: 'reset' })}>Reset</button>
    </div>
  );
}
```

**چه زمانی `useReducer` را به `useState` ترجیح دهیم:**

- وقتی state چند زیرمقدار دارد که با هم تغییر می‌کنند
- وقتی state بعدی به شکل‌های پیچیده‌ای به state قبلی وابسته است
- وقتی منطق update آن‌قدر پیچیده است که بهتر است در یک reducer خالص و قابل تست قرار بگیرد
- وقتی می‌خواهید همه transition های state را در یک جا متمرکز کنید
- وقتی می‌خواهید `dispatch` را به child ها پاس بدهید و update ها را به‌صورت action محور و شفاف نگه دارید

**تفاوت `useReducer` و Redux:** `useReducer` محلی است و داخل همان کامپوننت یا همراه با Context استفاده می‌شود. Redux یک store سراسری با middleware، DevTools و time-travel debugging فراهم می‌کند.

## 🧠 سوال 26

**شناسه**: react-026
**عنوان**: `useLayoutEffect` چیست و چه تفاوتی با `useEffect` دارد؟
**سطح دشواری**: سخت
**دسته‌بندی**: Effects و چرخه حیات

### پاسخ 📄

هر دو hook امضای یکسانی دارند، اما در زمان‌های متفاوتی از چرخه رندر اجرا می‌شوند.

**`useEffect`** — به‌صورت async بعد از این اجرا می‌شود که مرورگر صفحه را paint کرده باشد. یعنی کامپوننت رندر می‌شود، خروجی بصری روی صفحه می‌آید و بعد effect اجرا می‌شود.

**`useLayoutEffect`** — به‌صورت sync بعد از اینکه React تغییرات DOM را commit کرد اما قبل از paint شدن مرورگر اجرا می‌شود. تا وقتی effect تمام نشود، paint شدن صفحه متوقف می‌ماند.

```
React renders → React commits DOM mutations
  → useLayoutEffect runs (synchronously)
  → Browser paints
  → useEffect runs (asynchronously)
```

**چه زمانی از `useLayoutEffect` استفاده کنیم:**

- وقتی لازم است قبل از دیده شدن صفحه توسط کاربر، اندازه یا موقعیت DOM را بخوانید تا از flicker یا "نمایش اشتباه لحظه‌ای" جلوگیری شود

```jsx
function Tooltip({ targetRef, content }) {
  const tooltipRef = useRef(null);

  useLayoutEffect(() => {
    const targetRect = targetRef.current.getBoundingClientRect();
    const tooltip = tooltipRef.current;
    // قبل از paint مرورگر tooltip را در جای درست قرار بده
    tooltip.style.top = `${targetRect.bottom}px`;
    tooltip.style.left = `${targetRect.left}px`;
  });

  return (
    <div ref={tooltipRef} className="tooltip">
      {content}
    </div>
  );
}
```

**چه زمانی بهتر است از `useEffect` استفاده کنید:**

- برای هر چیزی که لازم نیست paint را block کند، مثل data fetching، subscription، analytics یا logging

**نکته مربوط به server-side rendering:** `useLayoutEffect` روی سرور اجرا نمی‌شود، چون DOM وجود ندارد، و همین باعث warning می‌شود. برای کامپوننت‌های سازگار با SSR از `useEffect` استفاده کنید یا با `typeof window !== 'undefined'` آن را شرطی کنید.

## 🧠 سوال 27

**شناسه**: react-027
**عنوان**: Error Boundary ها در React چیستند؟
**سطح دشواری**: متوسط
**دسته‌بندی**: کامپوننت‌ها

### پاسخ 📄

Error Boundary یک class component است که خطاهای جاوااسکریپتی در هرجای درخت child component هایش را می‌گیرد و به‌جای crash کردن کل اپلیکیشن، یک fallback UI نمایش می‌دهد.

Error boundary ها خطاها را در این موارد می‌گیرند:

- رندر
- متدهای lifecycle
- constructor های child component ها

اما این خطاها را نمی‌گیرند:

- event handler ها، که باید با `try/catch` مدیریت شوند
- کدهای async مثل `setTimeout` یا promise ها
- server-side rendering
- خطاهایی که در خود error boundary رخ می‌دهند

```jsx
class ErrorBoundary extends React.Component {
  state = { hasError: false, error: null };

  static getDerivedStateFromError(error) {
    // state را برای نمایش fallback UI به‌روزرسانی کن
    return { hasError: true, error };
  }

  componentDidCatch(error, info) {
    // لاگ کردن در سرویس گزارش خطا
    logError(error, info.componentStack);
  }

  render() {
    if (this.state.hasError) {
      return this.props.fallback ?? <h2>Something went wrong.</h2>;
    }
    return this.props.children;
  }
}

// استفاده
<ErrorBoundary fallback={<ErrorPage />}>
  <Dashboard />
</ErrorBoundary>;
```

خود Error Boundary ها همچنان در React به‌صورت class component پیاده‌سازی می‌شوند. در پروژه‌هایی که بیشتر با function component نوشته شده‌اند، خیلی از تیم‌ها از پکیج `react-error-boundary` برای داشتن wrapper آماده و الگوی سازگارتر با hook ها استفاده می‌کنند.

بخش‌های مختلف UI را در Error Boundary های جداگانه بپیچید تا خراب شدن یک بخش باعث از کار افتادن کل اپلیکیشن نشود.

## 🧠 سوال 28

**شناسه**: react-028
**عنوان**: Portal ها در React چیستند؟
**سطح دشواری**: متوسط
**دسته‌بندی**: کامپوننت‌ها

### پاسخ 📄

Portal فرزندان یک کامپوننت را در یک نود DOM متفاوت از نود والدش رندر می‌کند، در حالی که آن کامپوننت همچنان جای معمول خود را در درخت کامپوننت React حفظ می‌کند.

```jsx
import { createPortal } from 'react-dom';

function Modal({ isOpen, onClose, children }) {
  if (!isOpen) return null;

  return createPortal(
    <div className="modal-overlay" onClick={onClose}>
      <div className="modal-content" onClick={(e) => e.stopPropagation()}>
        {children}
      </div>
    </div>,
    document.body, // داخل document.body رندر می‌شود، نه داخل DOM والد
  );
}
```

**چرا Portal وجود دارد:**

ویژگی‌های CSS مثل `overflow: hidden`، `z-index` و `transform` روی ancestor ها می‌توانند UI هایی را که باید از والد خود "بیرون بزنند" قطع کنند یا در لایه اشتباه قرار دهند؛ مثل modal، tooltip، dropdown و notification.

**رفتارهای مهم:**

- **درخت React، نه درخت DOM** — حباب‌سازی event ها از سلسله‌مراتب React پیروی می‌کند، نه از سلسله‌مراتب DOM. یعنی کلیک داخل portal با اینکه در DOM جای دیگری است، در React به ancestor های خودش bubble می‌کند
- **Context کار می‌کند** — کامپوننت portal همچنان می‌تواند context را از والد React خودش بخواند
- **Lifecycle به والد React وابسته است** — وقتی والد unmount شود، محتوای portal هم cleanup می‌شود

```jsx
// محتوای Portal در DOM داخل document.body رندر می‌شود
// اما حباب‌سازی event در React از <Page> → <App> عبور می‌کند
function App() {
  return (
    <Page>
      <Modal>
        {' '}
        {/* والد React برابر Page است، والد DOM برابر body */}
        <button onClick={handleClose}>Close</button>
      </Modal>
    </Page>
  );
}
```

## 🧠 سوال 29

**شناسه**: react-029
**عنوان**: `useImperativeHandle` چیست و چه زمانی به `forwardRef` نیاز دارید؟
**سطح دشواری**: سخت
**دسته‌بندی**: Hooks

### پاسخ 📄

`forwardRef` یک wrapper است که به کامپوننت والد اجازه می‌دهد یک `ref` را تا DOM element یک child component یا یک imperative handle سفارشی عبور دهد.

به‌صورت پیش‌فرض، `ref` روی functional component ها کار نمی‌کند و ref فقط مستقیم به DOM element ها متصل می‌شود. `forwardRef` این امکان را می‌دهد که ref به functional component ها هم متصل شود.

```jsx
const FancyInput = forwardRef(function FancyInput(props, ref) {
  return <input ref={ref} className="fancy-input" {...props} />;
});

// Parent
function Form() {
  const inputRef = useRef(null);

  useEffect(() => {
    inputRef.current.focus(); // دسترسی مستقیم به DOM
  }, []);

  return <FancyInput ref={inputRef} />;
}
```

**`useImperativeHandle`** مشخص می‌کند والد از طریق ref دقیقا چه چیزی را ببیند. یعنی به‌جای DOM element خام، یک API محدود و کنترل‌شده در اختیار والد قرار می‌گیرد:

```jsx
const VideoPlayer = forwardRef(function VideoPlayer(props, ref) {
  const videoRef = useRef(null);

  useImperativeHandle(ref, () => ({
    play() {
      videoRef.current.play();
    },
    pause() {
      videoRef.current.pause();
    },
    seek(time) {
      videoRef.current.currentTime = time;
    },
    // خود videoRef.current با تمام DOM API آن مستقیما expose نمی‌شود
  }));

  return <video ref={videoRef} src={props.src} />;
});

// والد فقط { play, pause, seek } را می‌بیند
playerRef.current.play();
```

**چه زمانی استفاده کنیم:** با احتیاط. expose کردن یک API دستوری معمولا در مدل declarative ری‌اکت یک anti-pattern محسوب می‌شود. اولویت با پاس دادن state و callback از طریق props است. از `useImperativeHandle` زمانی استفاده کنید که واقعا لازم باشد والد عملی را به‌صورت imperative اجرا کند؛ مثل مدیریت focus، پخش media یا animation.

## 🧠 سوال 30

**شناسه**: react-030
**عنوان**: `React.lazy` چیست و همراه با `Suspense` چگونه کار می‌کند؟
**سطح دشواری**: متوسط
**دسته‌بندی**: بهینه‌سازی عملکرد

### پاسخ 📄

`React.lazy` امکان code splitting در سطح کامپوننت را فراهم می‌کند. این API یک `import()` پویا را wrap می‌کند و کامپوننتی lazy برمی‌گرداند که React فقط زمانی آن را بارگیری می‌کند که برای اولین بار رندر شود.

```jsx
import { lazy, Suspense } from 'react';

// باندل کامپوننت فقط وقتی Dashboard رندر شود دانلود می‌شود
const Dashboard = lazy(() => import('./Dashboard'));
const Settings = lazy(() => import('./Settings'));

function App() {
  const [page, setPage] = useState('dashboard');

  return (
    <Suspense fallback={<LoadingSpinner />}>
      {page === 'dashboard' ? <Dashboard /> : <Settings />}
    </Suspense>
  );
}
```

**نحوه کار:**

1. `React.lazy(() => import('./Dashboard'))` کامپوننتی می‌سازد که یک Promise را نگه می‌دارد
2. وقتی React برای اولین بار بخواهد آن lazy component را رندر کند، Promise را می‌خواند
3. اگر Promise هنوز pending باشد، React آن Promise را "throw" می‌کند و `<Suspense>` آن را می‌گیرد و fallback را نشان می‌دهد
4. وقتی Promise resolve شود و chunk دانلود شود، React دوباره رندر می‌کند

**نیازمندی‌ها:**

- `import()` پویا باید به ماژولی resolve شود که یک **default export** داشته باشد و آن export یک React component باشد
- باید در جایی بالاتر از lazy component یک مرز `<Suspense>` وجود داشته باشد

**ترکیب با React Router** برای route-level splitting:

```jsx
const Home = lazy(() => import('./pages/Home'));
const About = lazy(() => import('./pages/About'));

<Routes>
  <Route
    path="/"
    element={
      <Suspense fallback={<Spinner />}>
        <Home />
      </Suspense>
    }
  />
  <Route
    path="/about"
    element={
      <Suspense fallback={<Spinner />}>
        <About />
      </Suspense>
    }
  />
</Routes>;
```
