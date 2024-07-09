<!DOCTYPE html>
<html lang="ar">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Stop & Shop</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
            color: #333;
            margin: 0;
            padding: 20px;
            text-align: center;
        }
        header {
            background-color: #0073e6;
            color: white;
            padding: 10px 0;
        }
        h1 {
            margin: 0;
        }
        .container {
            max-width: 800px;
            margin: 20px auto;
            padding: 20px;
            background: white;
            box-shadow: 0 0 10px rgba(0,0,0,0.1);
        }
        .product-list, .add-product, .login-form, .register-form, .cart-container {
            text-align: left;
            margin-top: 20px;
        }
        .product, .login-form input, .login-form button, .register-form input, .register-form button {
            padding: 10px;
            margin-bottom: 10px;
            width: calc(100% - 20px);
            box-sizing: border-box;
        }
        .product {
            border-bottom: 1px solid #ddd;
            position: relative;
        }
        .product:last-child {
            border-bottom: none;
        }
        .add-to-cart-btn {
            position: absolute;
            right: 10px;
            bottom: 10px;
            padding: 5px 10px;
            background-color: #28a745;
            color: white;
            border: none;
            border-radius: 4px;
            cursor: pointer;
        }
        .add-to-cart-btn:hover {
            background-color: #218838;
        }
        footer {
            margin-top: 20px;
            color: #777;
        }
        input[type="text"], input[type="password"], input[type="number"] {
            width: calc(100% - 20px);
            padding: 8px;
            margin: 10px 0;
            border: 1px solid #ccc;
            border-radius: 4px;
        }
        button {
            padding: 10px 20px;
            border: none;
            background-color: #0073e6;
            color: white;
            cursor: pointer;
            border-radius: 4px;
        }
        button:hover {
            background-color: #005bb5;
        }
        .social-links {
            margin-top: 20px;
        }
        .social-links a {
            display: inline-block;
            margin: 0 10px;
            text-decoration: none;
            color: white;
            padding: 10px 20px;
            border-radius: 4px;
        }
        .whatsapp { background-color: #25D366; }
        .facebook { background-color: #3b5998; }
        .tiktok { background-color: #000000; }
        .scanner-container {
            display: none;
            margin-top: 20px;
        }
        #scanner {
            width: 100%;
        }
    </style>
</head>
<body>

<header>
    <h1>Stop & Shop</h1>
    <p>حاروف-حي البيدر -الشارع العام</p>
    <p>⏰ ساعات العمل: 8:00 صباحًا - 10:00 مساءً</p>
</header>

<!-- صفحة تسجيل الدخول -->
<div class="container" id="login-container">
    <h2>تسجيل دخول</h2>
    <div class="login-form">
        <h3>تسجيل دخول الموظفين</h3>
        <input type="text" id="employee-username" placeholder="اسم المستخدم" required>
        <input type="password" id="employee-password" placeholder="كلمة المرور" required>
        <button onclick="employeeLogin()">تسجيل دخول الموظفين</button>
    </div>
    <div class="login-form">
        <h3>تسجيل دخول الزبائن</h3>
        <input type="text" id="customer-username" placeholder="اسم المستخدم" required>
        <input type="password" id="customer-password" placeholder="كلمة المرور" required>
        <button onclick="customerLogin()">تسجيل دخول الزبائن</button>
    </div>
    <div class="register-form">
        <h3><a href="javascript:void(0);" onclick="registerCustomer()">تسجيل زبون جديد</a></h3>
    </div>
</div>

<!-- صفحة المنتجات للموظفين -->
<div class="container" id="employee-container" style="display: none;">
    <h2>المنتجات</h2>
    <div class="product-list" id="employee-product-list">
        <!-- سيتم إضافة المنتجات هنا -->
    </div>

    <h2>أضف منتج جديد</h2>
    <div class="add-product">
        <input type="text" id="product-name" placeholder="اسم المنتج" required>
        <input type="number" id="product-price" placeholder="السعر" required>
        <input type="text" id="product-barcode" placeholder="الباركود" required>
        <button onclick="addProduct()">إضافة</button>
    </div>
    <button onclick="goBackToLogin()">العودة إلى صفحة تسجيل الدخول</button>
</div>

<!-- صفحة المنتجات للزبائن -->
<div class="container" id="customer-container" style="display: none;">
    <h2>المنتجات والأسعار</h2>
    <div class="product-list" id="customer-product-list">
        <div class="search-form">
            <h3>البحث عن المنتجات</h3>
            <input type="text" id="search-input" placeholder="اسم المنتج" oninput="searchProducts()">
            <button onclick="startScanner()">مسح الباركود</button>
        </div>
        <!-- سيتم عرض المنتجات هنا -->
    </div>
    <div class="scanner-container" id="scanner-container">
        <h3>مسح الباركود</h3>
        <video id="scanner" style="width: 100%;"></video>
        <button onclick="stopScanner()">إيقاف المسح</button>
    </div>
    <h2>عربة التسوق</h2>
    <div class="cart-container" id="cart-container">
        <!-- سيتم عرض المنتجات في العربة هنا -->
    </div>
     <!-- إضافة زر تأكيد الطلب -->
   <div><a href="(STPNI1).html"><button onclick="calculateTotal()">احسب المجموع</button></a>
   
   </div>
    <button onclick="goBackToLogin()">العودة إلى صفحة تسجيل الدخول</button>
    
</div>

<div class="social-links">
    <a href="https://chat.whatsapp.com/your-whatsapp-group-link" class="whatsapp">WhatsApp</a>
    <a href="https://www.facebook.com/your-facebook-group-link" class="facebook">Facebook</a>
    <a href="https://www.tiktok.com/@your-tiktok-profile" class="tiktok">TikTok</a>
</div>

<footer>
    <p>📍 Harouf, Al baydar, Main Street</p>
</footer>

<script>
    const employeeProductList = document.getElementById('employee-product-list');
    const customerProductList = document.getElementById('customer-product-list');
    const loginContainer = document.getElementById('login-container');
    const employeeContainer = document.getElementById('employee-container');
    const customerContainer = document.getElementById('customer-container');
    const cartContainer = document.getElementById('cart-container');
    const scannerContainer = document.getElementById('scanner-container');

    let cart = [];

    // تحميل المنتجات والمستخدمين من التخزين المحلي عند تحميل الصفحة
    document.addEventListener('DOMContentLoaded', () => {
        loadProducts();
        loadCustomers();
    });

    // دالة تسجيل دخول الموظفين
    function employeeLogin() {
        const username = document.getElementById('employee-username').value;
        const password = document.getElementById('employee-password').value;

        // تحقق من بيانات الدخول
        if (username === 'admin' && password === '1234') {
            loginContainer.style.display = 'none';
            employeeContainer.style.display = 'block';
        } else {
            alert('اسم المستخدم أو كلمة المرور غير صحيحة');
        }
    }

    // دالة تسجيل دخول الزبائن
    function customerLogin() {
        const username = document.getElementById('customer-username').value;
        const password = document.getElementById('customer-password').value;

        // تحميل بيانات المستخدمين من التخزين المحلي
        let customers = localStorage.getItem('customers');
        customers = customers ? JSON.parse(customers) : [];

        // تحقق من بيانات الدخول
        const customer = customers.find(c => c.username === username && c.password === password);
        if (customer) {
            loginContainer.style.display = 'none';
            customerContainer.style.display = 'block';
        } else {
            alert('اسم المستخدم أو كلمة المرور غير صحيحة');
        }
    }

    // دالة تسجيل زبون جديد
    function registerCustomer() {
        const username = prompt('ادخل اسم المستخدم الجديد:');
        const password = prompt('ادخل كلمة المرور الجديدة:');
        
        if (username && password) {
            let customers = localStorage.getItem('customers');
            customers = customers ? JSON.parse(customers) : [];
            
            customers.push({ username, password });
            localStorage.setItem('customers', JSON.stringify(customers));
            
            alert('تم تسجيل الزبون بنجاح');
        } else {
            alert('يرجى ملء جميع الحقول');
        }
    }

    // دالة العودة إلى صفحة تسجيل الدخول
    function goBackToLogin() {
        employeeContainer.style.display = 'none';
        customerContainer.style.display = 'none';
        loginContainer.style.display = 'block';
    }

    // دالة لإضافة منتج جديد
    function addProduct() {
        const name = document.getElementById('product-name').value;
        const price = document.getElementById('product-price').value;
        const barcode = document.getElementById('product-barcode').value;

        if (name && price && barcode) {
            const product = { name, price, barcode };

            // إضافة المنتج إلى التخزين المحلي
            let products = localStorage.getItem('products');
            products = products ? JSON.parse(products) : [];
            products.push(product);
            localStorage.setItem('products', JSON.stringify(products));

            // تحديث قائمة المنتجات
            loadProducts();

            // إعادة تعيين الحقول
            document.getElementById('product-name').value = '';
            document.getElementById('product-price').value = '';
            document.getElementById('product-barcode').value = '';
        } else {
            alert('يرجى ملء جميع الحقول');
        }
    }

    // دالة لتحميل المنتجات من التخزين المحلي
    function loadProducts() {
        let products = localStorage.getItem('products');
        products = products ? JSON.parse(products) : [];

        // عرض المنتجات في قائمة الموظفين
        employeeProductList.innerHTML = '';
        products.forEach(product => {
            const productElement = document.createElement('div');
            productElement.className = 'product';
            productElement.innerHTML = `<strong>اسم المنتج:</strong> ${product.name}<br>
                                        <strong>السعر:</strong> ${product.price}<br>
                                        <strong>الباركود:</strong> ${product.barcode}`;
            employeeProductList.appendChild(productElement);
        });

        // عرض المنتجات في قائمة الزبائن
        customerProductList.innerHTML = '';
        products.forEach(product => {
            const productElement = document.createElement('div');
            productElement.className = 'product';
            productElement.innerHTML = `<strong>اسم المنتج:</strong> ${product.name}<br>
                                        <strong>السعر:</strong> ${product.price}<br>
                                        <strong>الباركود:</strong> ${product.barcode}
                                        <button class="add-to-cart-btn" onclick="addToCart('${product.name}', ${product.price})">إضافة إلى العربة</button>`;
            customerProductList.appendChild(productElement);
        });
    }

    // دالة لإضافة المنتجات إلى العربة
    function addToCart(name, price) {
        const product = { name, price };
        cart.push(product);
        updateCart();
    }

    // دالة لتحديث عرض العربة
    function updateCart() {
        cartContainer.innerHTML = '';
        cart.forEach((item, index) => {
            const cartItem = document.createElement('div');
            cartItem.className = 'product';
            cartItem.innerHTML = `<strong>اسم المنتج:</strong> ${item.name}<br>
                                  <strong>السعر:</strong> ${item.price}<br>
                                  <button class="add-to-cart-btn" onclick="removeFromCart(${index})">إزالة</button>`;
            cartContainer.appendChild(cartItem);
        });
    }

    // دالة لإزالة المنتجات من العربة
    function removeFromCart(index) {
        cart.splice(index, 1);
        updateCart();
    }

    // دالة لحساب المجموع النهائي
    function calculateTotal() {
        let total = cart.reduce((sum, item) => sum + item.price, 0);
        alert(`المجموع النهائي: ${total}`);
    }

    // دالة للبحث عن المنتجات
    function searchProducts() {
        const searchTerm = document.getElementById('search-input').value.toLowerCase();
        let products = localStorage.getItem('products');
        products = products ? JSON.parse(products) : [];

        customerProductList.innerHTML = '';
        const filteredProducts = products.filter(product => product.name.toLowerCase().includes(searchTerm));
        filteredProducts.forEach(product => {
            const productElement = document.createElement('div');
            productElement.className = 'product';
            productElement.innerHTML = `<strong>اسم المنتج:</strong> ${product.name}<br>
                                        <strong>السعر:</strong> ${product.price}<br>
                                        <strong>الباركود:</strong> ${product.barcode}
                                        <button class="add-to-cart-btn" onclick="addToCart('${product.name}', ${product.price})">إضافة إلى العربة</button>`;
            customerProductList.appendChild(productElement);
        });
    }

    // دالة لبدء مسح الباركود
    function startScanner() {
        scannerContainer.style.display = 'block';
        const scanner = document.getElementById('scanner');

        // استخدم مكتبة مثل QuaggaJS لمسح الباركود
        Quagga.init({
            inputStream: {
                name: "Live",
                type: "LiveStream",
                target: scanner    // Id of the element
            },
            decoder: {
                readers: ["code_128_reader", "ean_reader", "ean_8_reader", "code_39_reader", "code_39_vin_reader", "codabar_reader", "upc_reader", "upc_e_reader", "i2of5_reader"]
            }
        }, function (err) {
            if (err) {
                console.log(err);
                return;
            }
            Quagga.start();
        });

        Quagga.onDetected(function (data) {
            const barcode = data.codeResult.code;
            let products = localStorage.getItem('products');
            products = products ? JSON.parse(products) : [];
            const product = products.find(p => p.barcode === barcode);

            if (product) {
                alert(`تم العثور على المنتج: \nاسم المنتج: ${product.name}\nالسعر: ${product.price}`);
                stopScanner();
            } else {
                alert('لم يتم العثور على منتج بهذا الباركود');
            }
        });
    }

    // دالة لإيقاف مسح الباركود
    function stopScanner() {
        scannerContainer.style.display = 'none';
        Quagga.stop();
    }
</script>

</body>
</html>
<!DOCTYPE html>
<html lang="ar">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>تفاصيل الطلب</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
            color: #333;
            margin: 0;
            padding: 20px;
            text-align: center;
        }
        .container {
            max-width: 600px;
            margin: 0 auto;
            padding: 20px;
            background: white;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }
        input[type="text"], input[type="tel"] {
            width: calc(100% - 20px);
            padding: 10px;
            margin: 10px 0;
            border: 1px solid #ccc;
            border-radius: 4px;
        }
        button {
            padding: 10px 20px;
            border: none;
            background-color: #0073e6;
            color: white;
            cursor: pointer;
            border-radius: 4px;
        }
        button:hover {
            background-color: #005bb5;
        }
        a {
            display: block;
            margin-top: 20px;
            color: #0073e6;
            text-decoration: none;
        }
        a:hover {
            text-decoration: underline;
        }
    </style>
</head>
<body>
<div class="container">
    <h2>تفاصيل الطلب</h2>
    <input type="text" id="customer-name" placeholder="اسم الزبون" required>
    <input type="tel" id="customer-phone" placeholder="رقم الهاتف" required>
    <input type="text" id="customer-address" placeholder="مكان السكن" required>
    <input type="text" id="customer-home-address" placeholder="عنوان المنزل" required>
    <input type="text" id="customer-floor-number" placeholder="رقم الطابق" required>

    <!-- عربة التسوق -->
    <div id="shopping-cart" style="display: none;">
        <h3>عربة التسوق</h3>
        <ul id="cart-items">
            <!-- ستتم إضافة عناصر العربة هنا -->
        </ul>
        <button onclick="calculateTotal()">احسب المجموع</button>
    </div>

    <button onclick="addToCart()">إضافة المنتج إلى العربة</button>
    <button onclick="confirmOrder()">تأكيد الطلب</button>
    <a href="(STPNI).html"><h4>العودة إلى صفحة الشراء</h4></a>
</div>

<script>
    let shoppingCart = [];

    // دالة اضافة المنتج الى عربة التسوق
    function addToCart() {
        const productName = prompt('اسم المنتج:');
        const productPrice = parseFloat(prompt('سعر المنتج:'));

        if (productName && productPrice) {
            shoppingCart.push({ name: productName, price: productPrice });
            updateCartDisplay(); // تحديث عرض عربة التسوق
            document.getElementById('shopping-cart').style.display = 'block'; // عرض عربة التسوق بعد الإضافة الأولى
        } else {
            alert('يرجى إدخال اسم المنتج وسعره بشكل صحيح');
        }
    }

    // دالة لتحديث عرض عربة التسوق
    function updateCartDisplay() {
        const cartItemsElement = document.getElementById('cart-items');
        cartItemsElement.innerHTML = '';

        shoppingCart.forEach(item => {
            const li = document.createElement('li');
            li.textContent = `${item.name}: ${item.price} دولار`;
            cartItemsElement.appendChild(li);
        });
    }

    // دالة احساب المجموع
    function calculateTotal() {
        let totalAmount = 0;
        shoppingCart.forEach(item => {
            totalAmount += item.price;
        });

        const totalElement = document.createElement('p');
        totalElement.textContent = `المجموع: ${totalAmount} دولار`;
        
        const shoppingCartDiv = document.getElementById('shopping-cart');
        shoppingCartDiv.appendChild(totalElement);

        // إخفاء زر إضافة المنتج إلى العربة بعد حساب المجموع
        const addButton = document.querySelector('button[onclick="addToCart()"]');
        addButton.style.display = 'none';
    }

    // دالة تأكيد الطلب
    function confirmOrder() {
        const name = document.getElementById('customer-name').value;
        const phone = document.getElementById('customer-phone').value;
        const address = document.getElementById('customer-address').value;
        const homeAddress = document.getElementById('customer-home-address').value;
        const floorNumber = document.getElementById('customer-floor-number').value;

        if (name && phone && address && homeAddress && floorNumber && shoppingCart.length > 0) {
            // حساب مجموع الحساب
            let totalAmount = 0;
            shoppingCart.forEach(item => {
                totalAmount += item.price;
            });

            // إعداد تفاصيل الطلب
            let orderDetails = `اسم الزبون: ${name}\nرقم الهاتف: ${phone}\nمكان السكن: ${address}\nعنوان المنزل: ${homeAddress}\nرقم الطابق: ${floorNumber}\n\nتفاصيل الطلب:\n`;
            shoppingCart.forEach(item => {
                orderDetails += `${item.name}: ${item.price} دولار\n`;
            });
            orderDetails += `\nالمجموع: ${totalAmount} دولار`;

            // إعداد رسالة الواتساب للسوبر ماركت
            const supermarketPhoneNumber = '96181479786'; // رقم الهاتف للسوبر ماركت
            const supermarketMessage = orderDetails;
            const supermarketWhatsappUrl = `https://wa.me/${supermarketPhoneNumber}?text=${encodeURIComponent(supermarketMessage)}`;

            // فتح نافذة واتساب تلقائيًا للسوبر ماركت
            window.open(supermarketWhatsappUrl, '_blank');

            // إعداد رسالة الواتساب للزبون
            const driverPhoneNumber = '96181479786'; // رقم السائق الفعلي بدون علامة +
            const driverMessage = `تم تأكيد طلبك بنجاح!\n\n${orderDetails}`;
            const whatsappUrl = `https://wa.me/${driverPhoneNumber}?text=${encodeURIComponent(driverMessage)}`;

            // فتح نافذة واتساب تلقائيًا للزبون
            window.open(whatsappUrl, '_blank');
        } else {
            alert('يرجى ملء جميع الحقول وإضافة منتجات إلى عربة التسوق');
        }
    }
</script>
</body>
</html>

