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
<body class="bg-gray-100">
    <div class="max-w-md mx-auto bg-white min-h-screen shadow-lg flex flex-col">
        <header class="bg-blue-600 p-6 text-white text-center shadow-md">
            <h1 class="text-2xl font-bold">📚 تطبيق أنا عمر</h1>
            <p id="userName" class="text-sm mt-2 opacity-80"></p>
        </header>

        <div id="adminPanel" class="hidden p-4 bg-yellow-100 border-b-4 border-yellow-400">
            <h2 class="font-bold text-blue-800 mb-3">🛠 لوحة تحكم الإدارة</h2>
            <input id="sTitle" type="text" placeholder="عنوان القصة" class="w-full p-2 mb-2 border rounded">
            <input id="sPrice" type="number" placeholder="السعر" class="w-full p-2 mb-2 border rounded">
            <button onclick="addStory()" class="w-full bg-blue-600 text-white py-2 rounded font-bold shadow">إضافة القصة</button>
        </div>

        <main class="p-4 flex-grow">
            <div id="loginSection" class="text-center py-20 hidden">
                <button onclick="login()" class="bg-red-500 text-white px-8 py-3 rounded-full font-bold shadow-lg">تسجيل الدخول بجوجل</button>
            </div>
            <div id="storiesList" class="space-y-4">
                </div>
        </main>
    </div>

    <script>
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
        const adminEmail = "kemoloveone1234@gmail.com";

        function login() {
            const provider = new firebase.auth.GoogleAuthProvider();
            auth.signInWithPopup(provider);
        }

        auth.onAuthStateChanged(user => {
            if (user) {
                document.getElementById('loginSection').classList.add('hidden');
                document.getElementById('userName').innerText = "أهلاً " + user.displayName;
                if (user.email === adminEmail) {
                    document.getElementById('adminPanel').classList.remove('hidden');
                }
                loadStories();
            } else {
                document.getElementById('loginSection').classList.remove('hidden');
            }
        });

        function addStory() {
            const title = document.getElementById('sTitle').value;
            const price = document.getElementById('sPrice').value;
            if(!title || !price) return alert("اكتب البيانات");
            db.collection("stories").add({ title, price, time: new Date() });
            document.getElementById('sTitle').value = "";
            document.getElementById('sPrice').value = "";
        }

        function deleteStory(id) {
            if(confirm("هل تريد حذف هذه القصة؟")) {
                db.collection("stories").doc(id).delete();
            }
        }

        function loadStories() {
            db.collection("stories").orderBy("time", "desc").onSnapshot(snap => {
                const list = document.getElementById('storiesList');
                list.innerHTML = '';
                snap.forEach(doc => {
                    const s = doc.data();
                    const isAdmin = auth.currentUser.email === adminEmail;
                    list.innerHTML += `
                        <div class="bg-white p-4 rounded-xl shadow border relative">
                            <h3 class="font-bold text-lg">${s.title}</h3>
                            <p class="text-blue-600 font-bold">${s.price} جنيه</p>
                            <div class="flex gap-2 mt-3">
                                <a href="https://wa.me/201063858006?text=أريد شراء قصة: ${s.title}" class="flex-grow bg-green-500 text-white text-center py-1 rounded text-sm">طلب شراء</a>
                                ${isAdmin ? `<button onclick="deleteStory('${doc.id}')" class="bg-red-100 text-red-600 px-2 py-1 rounded text-xs">حذف</button>` : ''}
                            </div>
                        </div>`;
                });
            });
        }
    </script>
</body>
</html>
