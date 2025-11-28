🐾 小狗外卖饭盆 (Puppy Takeout Tracker)这是一个简单的单页应用（SPA），用于记录您吃过的外卖（或“零食”）及其价格和种类，并提供筛选和随机推荐功能。应用使用纯 HTML、JavaScript 和 Tailwind CSS（通过 CDN），并通过 Firebase Firestore 存储数据。🚀 部署到 Vercel/GitHub Pages由于本项目是纯静态 HTML/JS 应用，部署非常简单：创建 GitHub 仓库： 将 index.html 和 package.json 文件上传到您的 GitHub 仓库中。连接 Vercel： 登录 Vercel，选择 Import Git Repository，并连接到您刚才创建的仓库。配置： Vercel 会自动检测这是一个静态项目，无需任何构建配置。部署： 点击部署，您的应用将在几秒钟内部署完成。⚠️ 注意事项（重要）本项目依赖于一个外部的 Canvas 环境来提供 Firebase 的配置 (__firebase_config 等)。如果您要在 Vercel 或本地运行，您需要手动处理这部分配置。在 index.html 的 <script type="module"> 部分，找到以下代码：// --- GLOBAL VARIABLES (Canvas Environment Placeholders) ---
const appId = typeof __app_id !== 'undefined' ? __app_id : 'default-takeout-app';
const firebaseConfig = typeof __firebase_config !== 'undefined' ? JSON.parse(__firebase_config) : {};
const initialAuthToken = typeof __initial_auth_token !== 'undefined' ? __initial_auth_token : null;
// ... (Authentication logic uses these)
如果您想在 Vercel 上使用您自己的 Firestore 数据库，您需要：在 Firebase 控制台设置您的项目。获取您的 Firebase 配置对象（firebaseConfig）。将 index.html 中的这部分代码替换为您的实际配置，例如：// 替换为您的实际 Firebase 配置
const firebaseConfig = {
    apiKey: "YOUR_API_KEY",
    authDomain: "YOUR_AUTH_DOMAIN",
    projectId: "YOUR_PROJECT_ID",
    storageBucket: "YOUR_STORAGE_BUCKET",
    messagingSenderId: "YOUR_MESSAGING_SENDER_ID",
    appId: "YOUR_APP_ID"
};

// Vercel 部署不需要 Canvas 提供的 Auth Token 和 App ID，可以直接硬编码或使用环境变量。
const appId = firebaseConfig.projectId; // 可以使用 projectId 作为应用标识
const initialAuthToken = null; // 默认为 null，将匿名登录
✨ 应用功能🦴 记录零食： 记录名称、价格和种类。🔍 筛选想吃的： 按价格范围（如 ≈ 20 元）和类别（如鸡肉）筛选。🐕 随机抽选： 从当前筛选出的列表中随机挑选一个作为当天的食物推荐。
