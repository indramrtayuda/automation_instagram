from appium import webdriver
from appium.webdriver.common.appiumby import AppiumBy
from selenium.common.exceptions import NoSuchElementException
import subprocess
import shutil
import time





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


driver.implicitly_wait(50)
username = "usernameanda"
passwordbenar = "passwordanda"
passwordsalah = "asdfghjkl"

#Username dan email
username_field = driver.find_element(AppiumBy.XPATH, "/hierarchy/android.widget.FrameLayout/android.widget.LinearLayout/android.widget.FrameLayout/android.widget.LinearLayout/android.widget.FrameLayout/android.view.ViewGroup/android.widget.FrameLayout/android.widget.FrameLayout/android.widget.FrameLayout[2]/android.widget.FrameLayout[1]/android.view.ViewGroup/android.view.ViewGroup/android.view.ViewGroup/android.view.ViewGroup/android.view.ViewGroup[2]/android.view.ViewGroup/android.view.ViewGroup/android.widget.EditText")
username_field.send_keys(username)
print("Username berhasil di input")

password_field = driver.find_element(AppiumBy.XPATH, "/hierarchy/android.widget.FrameLayout/android.widget.LinearLayout/android.widget.FrameLayout/android.widget.LinearLayout/android.widget.FrameLayout/android.view.ViewGroup/android.widget.FrameLayout/android.widget.FrameLayout/android.widget.FrameLayout[2]/android.widget.FrameLayout[1]/android.view.ViewGroup/android.view.ViewGroup/android.view.ViewGroup/android.view.ViewGroup/android.view.ViewGroup[3]/android.view.ViewGroup/android.widget.EditText")
password_field.send_keys(passwordbenar)
print("Password berhasil di input")


# Klik tombol Login
x_coordinate = 354
y_coordinate = 884
driver.tap([(x_coordinate, y_coordinate)])
print("Berhasil Click button Login")
# Menunggu proses login selesai
time.sleep(10)   
    
try:
    element = driver.find_element(AppiumBy.XPATH,'//android.widget.ViewAnimator[@content-desc="Instagram Home feed"]/android.widget.LinearLayout/android.widget.ImageView')
    print("Login Success", element.text)
except NoSuchElementException:
    print("The password that you've entered is incorrect. Please try again.")
    
    
# Tutup sesi driver setelah selesai
driver.quit()
        




