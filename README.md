<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>تطبيق أنا عمر</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.1/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.1/firebase-auth-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.1/firebase-firestore-compat.js"></script>
</head>
<body class="bg-blue-50">
    <div class="max-w-md mx-auto bg-white min-h-screen shadow-2xl flex flex-col">
        <header class="bg-blue-600 p-6 text-white text-center shadow-lg">
            <h1 class="text-2xl font-bold">📚 تطبيق أنا عمر</h1>
            <p id="userNameDisplay" class="text-xs mt-2 opacity-80"></p>
        </header>

        <div id="adminPanel" class="hidden p-4 bg-yellow-100 border-b-4 border-yellow-400">
            <h2 class="font-bold text-red-600 mb-2">🛠 لوحة تحكم عمر</h2>
            <input id="sTitle" type="text" placeholder="اسم القصة" class="w-full p-2 mb-2 border rounded">
            <input id="sPrice" type="number" placeholder="السعر" class="w-full p-2 mb-2 border rounded">
            <button onclick="addStory()" class="bg-blue-600 text-white w-full py-2 rounded">إضافة قصة</button>
        </div>

        <main class="p-6 flex-grow">
            <div id="loginSection" class="text-center py-10">
                <h2 class="text-2xl font-bold mb-6">أهلاً بك في عالم المغامرة</h2>
                <button onclick="login()" class="bg-red-500 text-white px-10 py-4 rounded-full font-bold shadow-xl">G دخول بجوجل</button>
            </div>

            <div id="storiesList" class="grid grid-cols-1 gap-4">
                </div>
        </main>

        <footer class="p-4 border-t text-center bg-gray-50">
            <p class="text-sm">للتواصل: 01063858006</p>
        </footer>
    </div>

    <script>
        // بياناتك الخاصة التي أرسلتها
        const firebaseConfig = {
            apiKey: "AIzaSyBn-8ER3jyhEx6Fm4bM6uG9-fIoikHrT_c",
            authDomain: "ana-omar-b0e6c.firebaseapp.com",
            projectId: "ana-omar-b0e6c",
            storageBucket: "ana-omar-b0e6c.firebasestorage.app",
            messagingSenderId: "781802661336",
            appId: "1:781802661336:web:25736ef0b6b27f15167ead"
        };

        firebase.initializeApp(firebaseConfig);
        const auth = firebase.auth();
        const db = firebase.firestore();

        // إيميلك للتحكم (تأكد إنه نفس إيميل الجميل بتاعك)
        const myEmail = "kemoloveone1234@gmail.com"; 

        function login() {
            const provider = new firebase.auth.GoogleAuthProvider();
            auth.signInWithPopup(provider).catch(err => alert("تأكد من تفعيل Google في Firebase"));
        }

        auth.onAuthStateChanged(user => {
            if (user) {
                document.getElementById('loginSection').classList.add('hidden');
                document.getElementById('userNameDisplay').innerText = "أهلاً " + user.displayName;
                if (user.email === myEmail) {
                    document.getElementById('adminPanel').classList.remove('hidden');
                }
                loadStories();
            }
        });

        function addStory() {
            const title = document.getElementById('sTitle').value;
            const price = document.getElementById('sPrice').value;
            db.collection("stories").add({ title, price, time: new Date() });
            alert("تمت الإضافة!");
        }

        function loadStories() {
            db.collection("stories").orderBy("time", "desc").onSnapshot(snap => {
                const list = document.getElementById('storiesList');
                list.innerHTML = '';
                snap.forEach(doc => {
                    const s = doc.data();
                    list.innerHTML += `
                        <div class="bg-white p-4 rounded-xl shadow border">
                            <h3 class="font-bold">${s.title}</h3>
                            <p class="text-blue-600">${s.price} جنيه</p>
                            <button onclick="alert('تواصل مع عمر للدفع')" class="mt-2 text-xs bg-gray-100 p-1 rounded">شراء</button>
                        </div>`;
                });
            });
        }
    </script>
</body>
</html>
