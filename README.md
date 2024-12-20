# Selenium.
from selenium import webdriver
from time import sleep
from selenium.webdriver.common.by import By

file = open("log.txt","w")
driver = webdriver.Chrome()

def set_up():
    driver.get('http://www.saucedemo.com/')
    driver.maximize_window()
def login():
    user_name = driver.find_element(By.XPATH, '//input[@id="user-name"]')
    password = driver.find_element(By.XPATH, '//input[@id="password"]')

    login = "standard_user"
    Password = "secret_sauce"

    file.write("Success write login \n")

    user_name.send_keys(login)
    password.send_keys(Password)

    file.write("Success write password \n")
    sleep(2)
    login_butt = driver.find_element(By.XPATH, '//input[@id="login-button"]')
    login_butt.click()

def test_login_regirect():
    correkt_url = "https://www.saucedemo.com/inventory.html"
    get_url = driver.current_url

    assert correkt_url == get_url, "test_login_regirect is Failed"
    file.write("test_login_regirect is OK")
#//h4[text()="Password for all users:"]
#//div[@class= "form_group"][2]
def test_context_after_login_is_correct():
    correct_text = "Products"
    current_text = driver.find_element(By.XPATH,'//*[@id="header_container"]/div[2]/span')
    assert correct_text == current_text.text, "test_context_after_login_is_correct is Failed \n"
    file.write("test_context_after_login_is_correct is OK \n")

set_up()
login()

test_context_after_login_is_correct()
test_login_regirect()

file.close()
sleep(3)

