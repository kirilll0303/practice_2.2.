import urllib.request
import urllib.error

urls = [
    "https://github.com/",
    "https://www.binance.com/en",
    "https://tomtit.tomsk.ru/",
    "https://jsonplaceholder.typicode.com/",
    "https://moodle.tomtit-tomsk.ru/"

]

print("проверка доступности сайтов:")

for url in urls:
    try:
        req = urllib.request.Request(
            url, 
            headers={'User-Agent': 'Kirill03/10.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36'}
        )
        
        response = urllib.request.urlopen(req, timeout=10)
        code = response.getcode()
        
        if code == 200:
            status = "Доступен"
        elif code == 403:
            status = "Вход запрещен"
        elif code == 404:
            status = "Не найден"
        elif 500 <= code < 600:
            status = "Ошибка сервера"
        else:
            status = f"Другой статус ({code})"
            
    except urllib.error.HTTPError as e:
        code = e.code
        if code == 403:
            status = "Вход запрещен"
        elif code == 404:
            status = "Не найден"
        elif 500 <= code < 600:
            status = "Ошибка сервера"
        else:
            status = f"Ошибка {code}"
            
    except urllib.error.URLError as e:
        status = "Не доступен"
        code = "N/A"
    except Exception as e:
        status = f"Ошибка: {str(e)[:30]}..."
        code = "N/A"
    
    print(f"{url} – {status} – {code}")
