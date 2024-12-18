from selenium import webdriver

from selenium.webdriver.common.by import By

import pandas as pd

from time import sleep

# Selenium'u başlatma (Chrome tarayıcı kullanıyoruz)

driver = webdriver.Chrome()

# URL'ye gitme

url = "https://www.trendyol.com/sr?q=laptop&qt=laptop&st=laptop&os=1"

driver.get(url)

sleep(3)  # Sayfanın yüklenmesi için bekleme süresi

# Ürün isimlerini ve fiyatlarını çekme

urun_isimleri = driver.find_elements(By.XPATH, '//*[@id="search-app"]/div/div/div/div[2]/div[4]/div/div/div/div/div[1]/div/a/div[1]/div')

urun_fiyatlari = driver.find_elements(By.XPATH, '//*[@id="search-app"]/div/div/div/div[2]/div[4]/div/div/div/div/div[1]/div/div/div[1]')

# Liste oluşturma

liste = []

# Ürün isimleri ve fiyatlarını listeye ekleme

for isim, fiyat in zip(urun_isimleri, urun_fiyatlari):

    liste.append([isim.text.strip(), fiyat.text.strip()])

# DataFrame oluşturma

df = pd.DataFrame(liste, columns=["Ürün İsimleri", "Fiyatları"])

# DataFrame'i ekrana yazdırma

print(df)

# Tarayıcıyı kapatma

driver.quit()
