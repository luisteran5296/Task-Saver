```python
from selenium import webdriver
from selenium.webdriver.common.keys import Keys
from selenium.webdriver.common.by import By
from selenium.webdriver.common.action_chains import ActionChains
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
from selenium.common.exceptions import NoSuchElementException 
import time
import pandas as pd
```


```python
usuario = "luisteran5297@gmail.com"
cont = "12345678"
path = 'C:\Program Files (x86)\chromedriver.exe'
urlTodoist = 'https://todoist.com/es'
urlRandom = 'https://randomtodolistgenerator.herokuapp.com/library'

driver = webdriver.Chrome(path)
driver.get(urlRandom)
titulos = driver.find_elements_by_xpath("//div[@class='flexbox task-title']/div")
titulos = [elemento.text for elemento in titulos]
duracion = driver.find_elements_by_xpath("//div[@class='flexbox task-title']/span")
duracion = [elemento.text for elemento in duracion]
descripcion = driver.find_elements_by_class_name("card-text")
descripcion = [elemento.text for elemento in descripcion]

driver.execute_script("window.open()")
driver.switch_to.window(driver.window_handles[1])
driver.get(urlTodoist)
time.sleep(2)

search = driver.find_element_by_xpath("//div[@class='MTF3N _1lTj0']//ul[@class='_3XsmI']/li")
search.click()

app = WebDriverWait(driver, 10).until(
        EC.presence_of_element_located((By.CLASS_NAME, "standalone_page__frame"))
    )
search = app.find_element_by_id("email")
search.send_keys(usuario)
search = app.find_element_by_id("password")
search.send_keys(cont)
search.send_keys(Keys.RETURN)

app = WebDriverWait(driver, 10).until(
        EC.presence_of_element_located((By.ID, "app_holder"))
    )

for i in range(5):
    if (i==0):
        app.find_element_by_css_selector('.plus_add_button').click()    
    actions = ActionChains(driver)
    actions.send_keys(titulos[i])
    actions.perform()
    app.find_element_by_css_selector('[class="ist_button ist_button_red"]').click()
    time.sleep(2)
```


```python
tasks = pd.DataFrame({'Titulos':titulos, 'Duracion':duracion, 'Descripcion':descripcion})
tasks
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Titulos</th>
      <th>Duracion</th>
      <th>Descripcion</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>Eat two kinds of vegetable</td>
      <td>0.5hr</td>
      <td>Fiber contained in vegetables can reduce the r...</td>
    </tr>
    <tr>
      <td>1</td>
      <td>No suger drink</td>
      <td>0.5hr</td>
      <td>Too much sugar intake has negative impact on h...</td>
    </tr>
    <tr>
      <td>2</td>
      <td>Eat fruits</td>
      <td>0.5hr</td>
      <td>Two bananas/apples size fruits, or four plum s...</td>
    </tr>
    <tr>
      <td>3</td>
      <td>Go for a walk</td>
      <td>0.5hr</td>
      <td>Heading north, go for a walk and enjoy the sur...</td>
    </tr>
    <tr>
      <td>4</td>
      <td>Go for a walk</td>
      <td>0.5hr</td>
      <td>Heading south, go for a walk and enjoy the sur...</td>
    </tr>
    <tr>
      <td>5</td>
      <td>Go for a walk</td>
      <td>0.5hr</td>
      <td>Heading east, go for a walk and enjoy the surr...</td>
    </tr>
  </tbody>
</table>
</div>




```python

```
