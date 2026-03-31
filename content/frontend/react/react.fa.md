---
topic: react
language: fa
version: 1.1
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
