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


