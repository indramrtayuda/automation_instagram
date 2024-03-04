# Automation mobile app menggunakan python
## Test Positif dan Negatif Aplikasi Instagram

[![forthebadge made-with-python](http://ForTheBadge.com/images/badges/made-with-python.svg)](https://www.python.org/)

[![Ask Me Anything !](https://img.shields.io/badge/Ask%20me-anything-1abc9c.svg)](https://GitHub.com/Naereen/ama)

[![Made withJupyter](https://img.shields.io/badge/Made%20with-Jupyter-orange?style=for-the-badge&logo=Jupyter)](https://jupyter.org/try)

## Features
- Menjalankan end to end testing secara otomatis
- Menjalankan test positif dan negatif


## Tech
- [VScode] - Visual Studio Code adalah editor source code yang ringan, gratis, dan open source, yang dikembangkan oleh Microsoft. Alat ini biasanya digunakan untuk pengembangan web, tetapi mendukung banyak bahasa pemrograman dan memiliki berbagai extension yang tersedia.
- [Python] - Python adalah bahasa pemrograman yang banyak digunakan dalam aplikasi web, pengembangan perangkat lunak, ilmu data, dan machine learning (ML).
- [Appium Server] - Appium Server adalah komponen utama dari platform Appium. Ini adalah server yang berjalan di mesin lokal atau jarak jauh dan bertanggung jawab untuk menjalankan sesi pengujian otomatis dan mengirimkan perintah ke perangkat atau emulator yang sesuai
- [Appium Inspector] - Appium Inspector adalah alat grafis yang disediakan oleh Appium untuk membantu pengembang dan tester dalam mengeksplorasi dan menguji aplikasi mobile. Ini adalah antarmuka pengguna grafis (GUI) yang memungkinkan pengguna untuk melakukan berbagai tindakan di aplikasi mobile yang sedang diuj
- [Appium Python Client] - Library Python yang menyediakan antarmuka untuk berinteraksi dengan server Appium dalam pengujian otomatis aplikasi mobile menggunakan Python. Pustaka ini memungkinkan pengguna untuk menulis skrip pengujian otomatis yang dapat menjalankan perintah dan mengontrol aplikasi mobile yang sedang diuji melalui Appium Server.


## Requirement
- Python 3.9.11 or Later
- Appium-Python-Client 2.1.4 or Later
- Android SDK
- Appium Server
- Appium Inspector
- Real device android / Virtual device android

## Code
- Import library yang dibutuhkan untuk menjalankan automation mobile testing
```
from appium import webdriver
from appium.webdriver.common.appiumby import AppiumBy
from selenium.common.exceptions import NoSuchElementException
import subprocess
import shutil
import time
```
- deklarasikan aplikasi yang akan ditest, device yang digunakan, dan nomor udid pada device yang kita gunakan, lalu webdriver kita arahkan ke localhost dengan port default bawaan appium server yaitu 4723
```
caps = {
    "appPackage": "com.instagram.android",
    "appActivity": "com.instagram.mainactivity.InstagramMainActivity",
    "platformName": "android",
    "deviceName": "Galaxy A10",
    "udid": "RR8M9038Y7P",
    "automationName": "UiAutomator2",
    "newCommandTimeout": 36000,
    "noReset": "true"
    # "clearSystemFiles": True
}


driver = webdriver.Remote('http://127.0.0.1:4723/wd/hub', caps)
```


- perintah untuk memberi waktu delay pada driver yang sudah kita buat sebelumnya selama 50 detik (opsional). lalu kita buat variabel username, password yang benar dan password yang salah untuk kita inisialisasi di code berikutnya
```
driver.implicitly_wait(50)
username = "usernameanda"
passwordbenar = "passwordanda"
passwordsalah = "asdfghjkl"
```
- Membuat task untuk input username secara otomatis seperti dibawah ini. driver mencari element dengan menggunakan XPATH, Xpath itu sendiri kita dapatkan setelah kita koneksikan device android kita dengan appium inspector. Kemudiam beri perintah untuk memanggil variabel username yang sebelumnya sudah kita buat
```
username_field = driver.find_element(AppiumBy.XPATH, "/hierarchy/android.widget.FrameLayout/android.widget.LinearLayout/android.widget.FrameLayout/android.widget.LinearLayout/android.widget.FrameLayout/android.view.ViewGroup/android.widget.FrameLayout/android.widget.FrameLayout/android.widget.FrameLayout[2]/android.widget.FrameLayout[1]/android.view.ViewGroup/android.view.ViewGroup/android.view.ViewGroup/android.view.ViewGroup/android.view.ViewGroup[2]/android.view.ViewGroup/android.view.ViewGroup/android.widget.EditText")
username_field.send_keys(username)
print("Username berhasil di input")
```
- Membuat task untuk input password secara otomatis seperti dibawah ini. driver mencari element dengan menggunakan XPATH, Xpath itu sendiri kita dapatkan setelah kita koneksikan device android kita dengan appium inspector. Kemudiam beri perintah untuk memanggil variabel password yang sebelumnya sudah kita bua, disini kita kondisikan kita ingin testing positif atau negatif, jika ingin membuat positif test maka variabel yang dipanggil adalah password yang benar begitupun sebaliknya.
```
password_field = driver.find_element(AppiumBy.XPATH, "/hierarchy/android.widget.FrameLayout/android.widget.LinearLayout/android.widget.FrameLayout/android.widget.LinearLayout/android.widget.FrameLayout/android.view.ViewGroup/android.widget.FrameLayout/android.widget.FrameLayout/android.widget.FrameLayout[2]/android.widget.FrameLayout[1]/android.view.ViewGroup/android.view.ViewGroup/android.view.ViewGroup/android.view.ViewGroup/android.view.ViewGroup[3]/android.view.ViewGroup/android.widget.EditText")
password_field.send_keys(passwordbenar)
print("Password berhasil di input")
```
- Jika mengalami kesulitan menggunakan mengambil element dari XPATH, ID dan lain lain. Code ini adalah perintah untuk melakukan click button login dengan menggunakan titik koordinat X,Y pada device android yang bertujuan untuk testing apakah fungsi button login dapat berfungsi dengan baik atau tidak
```
x_coordinate = 354
y_coordinate = 884
driver.tap([(x_coordinate, y_coordinate)])
print("Berhasil Click button Login")
```
- Code ini berguna untuk memberi kesempatan pada aplikasi untuk menyelesaikan proses login agar halaman berikutnya pada aplikasi terlihat dahulu sehingga kita bisa memvalidasi apakah login kita sudah sukses atau belum
```
time.sleep(10) 
```
- Code dibawah ini berfungsi untuk memvalidasi apakah testing yang kita buat sudah berhasil kedalam dashboard aplikasi atau belum. karena aplikasi yang sudah berhasil login maka akan masuk kedalam menu utama / dashboard aplikasi. 
```
try:
    element = driver.find_element(AppiumBy.XPATH,'//android.widget.ViewAnimator[@content-desc="Instagram Home feed"]/android.widget.LinearLayout/android.widget.ImageView')
    print("Login Success", element.text)
except NoSuchElementException:
    print("The password that you've entered is incorrect. Please try again.")
```
- Tutup aplikasi jika sudah selesai dijalankan
```
driver.quit()
```

