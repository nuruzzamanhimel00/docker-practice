This is a [Next.js](https://nextjs.org) project bootstrapped with [`create-next-app`](https://nextjs.org/docs/app/api-reference/cli/create-next-app).

## Getting Started

First, run the development server:

```bash
npm run dev
# or
yarn dev
# or
pnpm dev
# or
bun dev
```

Open [http://localhost:3000](http://localhost:3000) with your browser to see the result.

You can start editing the page by modifying `app/page.tsx`. The page auto-updates as you edit the file.

This project uses [`next/font`](https://nextjs.org/docs/app/building-your-application/optimizing/fonts) to automatically optimize and load [Geist](https://vercel.com/font), a new font family for Vercel.

## Learn More

To learn more about Next.js, take a look at the following resources:

- [Next.js Documentation](https://nextjs.org/docs) - learn about Next.js features and API.
- [Learn Next.js](https://nextjs.org/learn) - an interactive Next.js tutorial.

You can check out [the Next.js GitHub repository](https://github.com/vercel/next.js) - your feedback and contributions are welcome!

## Deploy on Vercel

The easiest way to deploy your Next.js app is to use the [Vercel Platform](https://vercel.com/new?utm_medium=default-template&filter=next.js&utm_source=create-next-app&utm_campaign=create-next-app-readme) from the creators of Next.js.

Check out our [Next.js deployment documentation](https://nextjs.org/docs/app/building-your-application/deploying) for more details.

## Docker Project Run Guide (ChatGPT Reference)

* 🔗 **ChatGPT Shared Discussion:** [Docker Project Run Guide (Full Chat)](https://chatgpt.com/share/6a83bcd7-8be0-83ee-b1a0-bc71ca7257ef)

নিচে চ্যাটজিপিটি আলোচনা থেকে প্রজেক্টটি ডকারাইজ করার এবং রান করার বিস্তারিত গাইড তুলে ধরা হলো:

### ১. প্রজেক্ট ফোল্ডারে যাওয়া (Project Folder)
PowerShell বা Terminal খুলে প্রজেক্ট ফোল্ডারে প্রবেশ করুন:
```powershell
cd "D:\laragon\www\docker practice\my-app"
```
প্রজেক্টের ফাইলগুলো চেক করতে রান করুন:
```powershell
dir
```

### ২. ডকার সক্রিয় আছে কিনা তা যাচাই করা
ডকার সার্ভিস সচল আছে কিনা তা চেক করুন:
```powershell
docker --version
docker info
```
যদি কোনো এরর আসে, তাহলে প্রথমে আপনার সিস্টেমে **Docker Desktop** চালু করে নিন।

### ৩. বেস ইমেজ পুল করা (Base Image Pull)
প্রজেক্টের Dockerfile অনুযায়ী `node:20-alpine` ইমেজটি ডাউনলোড করতে রান করুন:
```powershell
docker pull node:20-alpine
```
*(দ্রষ্টব্য: manually `docker pull` করা বাধ্যতামূলক নয়। `docker build` করার সময় ডকার নিজে থেকেই এটি ডাউনলোড করে নেবে, তবে আগে থেকে পুল করে রাখা ভালো।)*

ডাউনলোড করা ইমেজগুলোর তালিকা দেখতে:
```powershell
docker images
```

### ৪. ডকার ইমেজ বিল্ড করা (Docker Image Build)
ইমেজ বিল্ড করার জন্য নিচের কমান্ডটি রান করুন (ইমেজের নাম `my-app` দেওয়া হয়েছে):
```powershell
docker build -t my-app .
```

### ৫. কন্টেইনার রান করা (Container Run)
বিল্ড করা ইমেজ থেকে কন্টেইনার রান করতে নিচের কমান্ডটি ব্যবহার করুন:
```powershell
docker run -d --name my-app -p 3000:3000 my-app
```
এখানে:
- `-d` কন্টেইনারটিকে ব্যাকগ্রাউন্ডে রান করবে।
- `--name my-app` কন্টেইনারের নাম সেট করবে।
- `-p 3000:3000` আপনার লোকাল কম্পিউটারের `3000` পোর্টকে কন্টেইনারের `3000` পোর্টের সাথে কানেক্ট করবে।

কন্টেইনারটি সচল আছে কিনা তা দেখতে রান করুন:
```powershell
docker ps
```

### ৬. প্রজেক্ট ব্রাউজ করা
ব্রাউজার ওপেন করে এই লিংকে যান:
```text
http://localhost:3000
```

---

### কন্টেইনার ও ইমেজ ম্যানেজমেন্টের প্রয়োজনীয় কমান্ডসমূহ

* **কন্টেইনারের লগ দেখা (Container Logs):**
  ```powershell
  docker logs my-app
  # লাইভ লগ দেখতে:
  docker logs -f my-app
  ```
* **কন্টেইনার বন্ধ করা (Stop Container):**
  ```powershell
  docker stop my-app
  ```
* **কন্টেইনার পুনরায় চালু করা (Start Container):**
  ```powershell
  docker start my-app
  ```
* **কন্টেইনার পার্মানেন্টলি ডিলিট করা (Remove Container):**
  ```powershell
  docker rm my-app
  ```
* **ডকার ইমেজ ডিলিট করা (Remove Image):**
  ```powershell
  docker rmi my-app
  ```
* **যেকোনো এরর ডিবাগ করতে:**
  ```powershell
  docker ps -a
  docker logs my-app
  docker images
  ```

> [!IMPORTANT]
> Dockerfile-এ Next.js-এর `standalone` আউটপুট ব্যবহার করা হচ্ছে। তাই আপনার `next.config.ts`-এ `output: 'standalone'` কনফিগারেশন থাকা আবশ্যক।


## Docker Hot Reload & Volumes Guide (Antigravity Guide)

এখানে ডকার ভলিউম (Volumes), হট-রিলোড (Hot Reloading), ডেভেলপমেন্ট এনভায়রনমেন্ট কনফিগারেশন এবং সকল প্রয়োজনীয় কমান্ডের বিস্তারিত গাইড দেওয়া হলো:

---

### 📌 প্রশ্ন ০১: Docker-এ "Volumes" কী জিনিস? আমি লোকাল কোড চেঞ্জ করলে কন্টেইনারে সরাসরি রিফ্লেক্ট (হট-রিলোড) হবে কীভাবে?

#### **১. Docker Volumes কী?**
ডকার কন্টেইনারের ভেতরের ফোল্ডার/ফাইলকে আপনার নিজের লোকাল কম্পিউটার (Host Machine)-এর ফোল্ডারের সাথে কানেক্ট বা লিঙ্ক করার মেকানিজমকে **Docker Volumes** বলা হয়। 

সাধারণত কন্টেইনার ডিলিট করে দিলে তার ভেতরের সমস্ত ডাটা বা কোড ডিলিট হয়ে যায়। কিন্তু ভলিউম (Bind Mount) ব্যবহার করলে:
* **ডাটা সুরক্ষিত থাকে (Data Persistence):** কন্টেইনার ডিলিট করলেও ফাইল বা ডাটা লোকাল মেশিনে থেকে যায়।
* **কোড রিয়েল-টাইম সিঙ্ক হয়:** আপনার কম্পিউটারের কোড ফাইল চেঞ্জ করার সাথে সাথে কন্টেইনারের ভেতরের ফাইলও আপডেট হয়ে যায়।

#### **২. রিয়েল-টাইম আপডেট দেখার কাজের ধাপসমূহ:**
ডেভেলপমেন্ট মোডে কন্টেইনার চালনা এবং ভলিউম লিঙ্ক করার জন্য প্রজেক্টে ২টি ফাইল তৈরি করা হয়েছে:
1. **[`Dockerfile.dev`](file:///D:/laragon/www/docker practice/my-app/Dockerfile.dev)** (ডেভেলপমেন্টের জন্য ডকারফাইল)
2. **[`docker-compose.yml`](file:///D:/laragon/www/docker practice/my-app/docker-compose.yml)** (ভলিউম এবং পোর্ট ম্যানেজ করার ফাইল)

**রান করার কমান্ডসমূহ:**
1. **পুরাতন কন্টেইনার বন্ধ করুন (যদি থাকে):**
   ```powershell
   docker compose down
   ```
2. **ডকার কম্পোজ ব্যবহার করে ইমেজ বিল্ড ও রান করুন:**
   ```powershell
   docker compose up --build
   ```
3. **ব্রাউজারে চেক করুন:** [http://localhost:3000](http://localhost:3000) ওপেন করে কোড চেঞ্জ করুন, সাথে সাথে লাইভ আপডেট দেখতে পাবেন।

---

### 📌 প্রশ্ন ০২: ডেভেলপমেন্টের ফাইলগুলোতে (Dockerfile.dev এবং docker-compose.yml) কী কী কাজ করা হয়েছে?

#### **১. [`Dockerfile.dev`](file:///D:/laragon/www/docker practice/my-app/Dockerfile.dev) ফাইলের কাজ:**
* **`FROM node:20-alpine`:** লাইটওয়েট নোড বেস ইমেজ সেট করা হয়েছে।
* **`WORKDIR /app`:** কন্টেইনারের ভেতরে কাজের মেইন ফোল্ডার `/app` নির্ধারণ করা হয়েছে।
* **`RUN npm install`:** লোকাল প্রজেক্টের লাইব্রেরিগুলো কন্টেইনারে ইনস্টল করা হয়েছে।
* **`CMD ["npm", "run", "dev", "--", "--webpack"]`:** Next.js ডেভেলপমেন্ট সার্ভারটি **Webpack** কম্পাইলার ব্যবহার করে চালু করা হচ্ছে (যা উইন্ডোজে হট-রিলোড পোলিং নিশ্চিত করে)।

#### **২. [`docker-compose.yml`](file:///D:/laragon/www/docker practice/my-app/docker-compose.yml) ফাইলের কাজ:**
* **`volumes: - .:/app` (Bind Mount):** লোকাল কম্পিউটারের ফাইল কন্টেইনারের সাথে লিঙ্ক করা হয়েছে।
* **`volumes: - /app/node_modules` এবং `- /app/.next`:** কন্টেইনারের নিজস্ব লাইব্রেরি ও ক্যাশ যেন লোকাল ফাইল দ্বারা মুছে না যায় তা নিশ্চিত করা হয়েছে।
* **`environment:`**
  * `WATCHPACK_POLLING=true` -> উইন্ডোজ ফাইল পরিবর্তন ডিটেক্ট করার পোলিং সার্ভিস অন করে।
  * `HOSTNAME=0.0.0.0` -> ডকার কন্টেইনারের বাইরে থেকে সংযোগ গ্রহণ নিশ্চিত করে।
  * `PORT=3000` -> অ্যাপের পোর্ট ৩০০০ নির্ধারণ করে।

---

### 📌 প্রশ্ন ০৩: Ctrl + C দিয়ে বন্ধ (Stop) করার পর পুনরায় কীভাবে প্রজেক্ট চালু করব?

যদি আপনি টার্মিনালে **`Ctrl + C`** চেপে ডকার কম্পোজ বন্ধ করে দেন, তবে পুনরায় চালু করতে জাস্ট নিচের কমান্ডটি দিন:
```powershell
docker compose up
```

#### **গুরুত্বপূর্ণ নোট:**
* **পুনরায় `--build` দেওয়ার দরকার নেই:** যেহেতু লোকাল সোর্স কোড ভলিউম দিয়ে লিঙ্ক করা আছে, তাই সাধারণ কোড পরিবর্তনের জন্য নতুন করে ইমেজ বিল্ড করার প্রয়োজন হয় না। এটি সরাসরি লোকাল ফাইল থেকেই রিয়েল-টাইম আপডেট নেয়।
* **কখন `--build` দিতে হবে:** শুধুমাত্র তখনই `--build` ব্যবহার করবেন যখন আপনি নতুন কোনো NPM Package ইনস্টল করবেন (অর্থাৎ `package.json` ফাইলে কোনো পরিবর্তন আসবে)। যেমন:
  ```powershell
  docker compose up --build
  ```

---

### 📌 প্রশ্ন ০৪: প্রথমবার রান করার পর `localhost:3000` লোড হচ্ছিল না এবং ফাইল চেঞ্জ সেভ করলে অটো-আপডেট হচ্ছিল না কেন? সমাধান কী?

#### **১. পোর্ট কানেকশন এরর সমাধান (HOSTNAME=0.0.0.0):**
* **সমস্যা:** Next.js ১৫/১৬ ডিফল্টভাবে শুধু কন্টেইনারের ভেতরের লোকালহোস্টে রিকোয়েস্ট রিসিভ করে। ফলে হোস্ট মেশিন (আপনার কম্পিউটার) থেকে অ্যাক্সেস করা যাচ্ছিল না।
* **সমাধান:** ডকার কম্পোজ ফাইলের এনভায়রনমেন্টে `HOSTNAME=0.0.0.0` অ্যাড করে ডকারকে বলা হয়েছে যেকোনো নেটওয়ার্ক ইন্টারফেস থেকে আগত রিকোয়েস্ট কন্টেইনারের ভেতর কানেক্ট করতে দিতে।

#### **২. হট-রিলোড না হওয়ার সমাধান (Turbopack বনাম Webpack):**
* **সমস্যা:** উইন্ডোজের ডকার ভলিউমগুলোতে ফাইল পরিবর্তন সনাক্ত করার নেটিভ সিগন্যাল (`inotify` events) মাঝে মাঝে কাজ করে না। এই সমস্যা সমাধানের জন্য Webpack-এর পোলিং ফিচার (`WATCHPACK_POLLING=true`) সাহায্য করে। কিন্তু Next.js ১৫/১৬ এর নতুন **Turbopack** কম্পাইলার বর্তমানে পোলিং সাপোর্ট করে না।
* **সমাধান:** আমরা ডেভেলপমেন্ট ডকারফাইলে Next.js-কে Turbopack ছাড়া প্রথাগত Webpack-এ রান করতে বাধ্য করেছি (`next dev --webpack` কমান্ডের মাধ্যমে)। এখন Webpack পোলিং পদ্ধতিতে প্রতি সেকেন্ডে ফাইল চেক করে লোকাল কোড চেঞ্জ সনাক্ত করতে পারে এবং ইনস্ট্যান্টলি ব্রাউজারে হট-রিলোড সম্পন্ন করে।

---

### 📌 প্রশ্ন ০৫: `docker compose up --build` রান করার পর বন্ধ করে আবার `docker compose up` দিলে আসলে কোন কোন ফাইলে কাজ হয়? মূল `dockerfile` ফাইলের কি তখন কোনো ভূমিকা থাকে?

#### **১. কোন কোন ফাইলের কাজ হয়?**
যখন আপনি `docker compose up` রান করেন, ডকার কম্পোজ মূলত নিচের ফাইলগুলো নিয়ে কাজ করে:
* **[`docker-compose.yml`](file:///D:/laragon/www/docker practice/my-app/docker-compose.yml):** ডকার কম্পোজ প্রথমে এই ফাইলটি লোড করে এর কনফিগারেশন (পোর্ট, ভলিউম, এনভায়রনমেন্ট ভেরিয়েবল) পড়ে নেয়।
* **[`Dockerfile.dev`](file:///D:/laragon/www/docker practice/my-app/Dockerfile.dev):** ডকার কম্পোজ ফাইলে আমরা স্পষ্ট করে বলে দিয়েছি যেন সে ডেভেলপমেন্টের জন্য `Dockerfile.dev` ব্যবহার করে। তাই এই ফাইলটির ইনস্ট্রাকশনগুলো কাজ করে।
* **আপনার লোকাল সোর্স কোড ফাইলসমূহ (`app/`, `package.json` ইত্যাদি):** যেহেতু ডকার ভলিউমের মাধ্যমে লোকাল ডিরেক্টরি মাউন্ট করা আছে, তাই ডকার কন্টেইনার রান করার সময় আপনার কম্পিউটারের লোকাল ফাইলগুলো থেকেই সরাসরি কোড নিয়ে চালনা করে।

#### **২. মূল `dockerfile` এর ভূমিকা কী তখন?**
* **কোনো ভূমিকা থাকে না।**
* এই সময়ে প্রজেক্টের রুট ডিরেক্টরিতে থাকা মূল [`dockerfile`](file:///D:/laragon/www/docker practice/my-app/dockerfile) (যেটি প্রোডাকশন বিল্ডের জন্য তৈরি) সম্পূর্ণ নিষ্ক্রিয়া ও অব্যবহৃত অবস্থায় থাকে। এটি কেবল তখনই কাজ করে যখন আপনি প্রোডাকশন বিল্ড দিতে চান (যেমন সার্ভারে অ্যাপ ডিপ্লয় করার সময়)।

---

### 📌 প্রশ্ন ০৬: রানিং ডকার কন্টেইনার বন্ধ (Stop/Down) করার সঠিক কমান্ডগুলো কী কী? এগুলো কখন এবং কীভাবে চালাব?

কন্টেইনার বন্ধ করার জন্য মূলত দুটি পদ্ধতি ব্যবহার করা যায়। নিচে বিস্তারিত গাইড দেওয়া হলো:

#### **পদ্ধতি ১: Docker Compose ব্যবহার করে (সবচেয়ে সহজ ও রেকমেন্ডেড)**
যদি আপনি `docker compose up` দিয়ে প্রজেক্ট চালু করে থাকেন, তবে প্রজেক্ট ডিরেক্টরিতে টার্মিনাল ওপেন করে নিচের কমান্ডগুলোর যেকোনো একটি রান করতে পারেন:

* **কন্টেইনার সাময়িকভাবে বন্ধ করতে:**
  ```powershell
  docker compose stop
  ```
  * **কখন চালাবেন:** যখন আপনি সাময়িকভাবে কাজ বন্ধ রাখতে চান এবং পরবর্তীতে আবার দ্রুত সার্ভার চালু করতে চান। এতে কন্টেইনার ও ডাটা ডিলিট হয় না, শুধু রানিং প্রসেসটি বন্ধ হয়।
  
* **কন্টেইনার বন্ধ করে মেমোরি খালি করতে:**
  ```powershell
  docker compose down
  ```
  * **কখন চালাবেন:** দিনের কাজ শেষ করে কন্টেইনার পুরোপুরি বন্ধ করে ডিলিট করতে চাইলে এটি চালাবেন। এটি কন্টেইনার বন্ধ করার পাশাপাশি নেটওয়ার্ক ও তৈরি হওয়া অন্যান্য রিসোর্সগুলো রিমুভ করে পিসির পোর্ট ও মেমোরি খালি করে।

---

#### **পদ্ধতি ২: Docker CLI ব্যবহার করে (নির্দিষ্ট কোনো কন্টেইনার বন্ধ করতে)**
যদি কোনো কন্টেইনার ব্যাকগ্রাউন্ডে রান হয়ে থাকে বা ডকার কম্পোজ ছাড়া সরাসরি স্টার্ট করা হয়ে থাকে, তবে নিচের ধাপগুলো অনুসরণ করুন:

1. **প্রথমে রানিং কন্টেইনারের লিস্ট দেখুন:**
   ```powershell
   docker ps
   ```
   এই কমান্ডটি দিলে রানিং কন্টেইনারগুলোর **CONTAINER ID** এবং **NAMES** দেখতে পাবেন (যেমন: `my-app-web-1`)।

2. **নির্দিষ্ট কন্টেইনারটি বন্ধ করুন:**
   * **নাম (Name) ব্যবহার করে:**
     ```powershell
     docker stop my-app-web-1
     ```
   * **আইডি (ID) ব্যবহার করে:**
     ```powershell
     docker stop a4991abad14f
     ```
     *(আইডি হিসেবে `docker ps` এ পাওয়া আইডি-টি ব্যবহার করবেন)*
   * **কখন চালাবেন:** যখন আপনার পোর্টের অ্যাক্সেস ব্লক হয়ে থাকে (যেমন: পোর্ট ৩০০০ অলরেডি ইউজড) অথবা কোনো কন্টেইনার ব্যাকগ্রাউন্ডে চলতে থাকে এবং তার প্রজেক্ট ডিরেক্টরি আপনার কাছে ওপেন না থাকে, তখন এই কমান্ড দিয়ে সরাসরি বন্ধ করে দিতে পারেন।

---

### 🛠️ ডকার ও কম্পোজ ব্যবহারের প্রয়োজনীয় কমান্ড বুক (Quick Command Reference)


| কমান্ড | কাজ | কখন ব্যবহার করবেন |
| :--- | :--- | :--- |
| `docker compose up --build` | ইমেজ নতুন করে বিল্ড করে কন্টেইনার রান করে। | প্রথমবার প্রজেক্ট সেটআপের সময় অথবা `package.json` চেঞ্জ হলে। |
| `docker compose up` | পূর্বের তৈরি ইমেজের সাহায্যে কন্টেইনার রান করে। | যেকোনো সাধারণ কোড পরিবর্তনের পর দ্রুত ডেভেলপমেন্ট সার্ভার চালু করতে। |
| `docker compose down` | কম্পোজের মাধ্যমে তৈরি হওয়া কন্টেইনার ও নেটওয়ার্ক বন্ধ করে ডিলিট করে। | সম্পূর্ণ কাজ শেষে পিসির পোর্ট ও মেমোরি খালি করতে। |
| `docker compose logs` | রানিং কন্টেইনারের কনসোল আউটপুট বা লগ দেখায়। | কোনো এরর আসলে বা সার্ভার ঠিকমতো চালু হয়েছে কিনা তা দেখতে। |
| `docker ps` | বর্তমানে আপনার কম্পিউটারে রানিং ডকার কন্টেইনারগুলোর লিস্ট দেখায়। | পোর্ট ৩০০০ অন্য কোনো কন্টেইনার দ্বারা ব্লক কিনা চেক করতে। |
| `docker stop <container_name>` | নির্দিষ্ট একটি কন্টেইনার বন্ধ করে। | কোনো কন্টেইনার ব্যাকগ্রাউন্ডে চলতে থাকলে তা থামাতে। |
| `docker rm <container_name>` | বন্ধ থাকা কন্টেইনার ডিলিট করে। | একই নামে নতুন কন্টেইনার রান করার জন্য আগের কন্টেইনারটি ডিলিট করতে। |

---




