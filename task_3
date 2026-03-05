import requests
import json
import os

file = "save.json"

def load_data():
    try:
        data = requests.get("https://www.cbr-xml-daily.ru/daily_json.js", 
                           headers={'User-Agent': 'Kirill03'}, timeout=10).json()
        return data.get("Valute", {})
    except:
        return {}

def show_currency(code, curr):
    print(f"\n{code} ({curr.get('Name','')}): {curr.get('Value',0):.2f} руб. (изм: {curr.get('Value',0)-curr.get('Previous',0):+.4f})")

def load_groups():
    return json.load(open(file)) if os.path.exists(file) else {}

def save_groups(g):
    json.dump(g, open(file, 'w+'), ensure_ascii=False, indent=2)

data = load_data()
if not data: exit("Ошибка загрузки")

groups = load_groups()
print(f"Групп загружено: {len(groups)}")

while True:
    print("\n1.Все валюты 2.Поиск 3.Группы 4.Сохранить 5.Выход")
    cmd = input("Выбор: ")

    if cmd == "1":
        for code, curr in sorted(data.items()):
            show_currency(code, curr)
    elif cmd == "2":
        code = input("Code: ").upper()
        show_currency(code, data[code]) if code in data else print("Не найдено")
    elif cmd == "3":
        while True:
            print("\n1.Создать 2.Список 3.Изменить 4.Назад")
            sc = input("Выбор: ")
            if sc == "1":
                name = input("Name group: ")
                if name: groups[name] = []; print(f"OK {name}")
            elif sc == "2":
                for name, items in groups.items():
                    print(f"\n{name}: {', '.join(items) if items else 'пусто'}")
                    for code in items:
                        if code in data: print(f"  {code}: {data[code]['Value']:.4f}")
            elif sc == "3":
                name = input("Group: ")
                if name in groups:
                    a = input("add/del: ").lower()
                    code = input("Code: ").upper()
                    if a == "add" and code in data and code not in groups[name]:
                        groups[name].append(code)
                    elif a == "del" and code in groups[name]:
                        groups[name].remove(code)
                    print("OK")
            elif sc == "4":
                break
    elif cmd == "4":
        save_groups(groups)
    elif cmd == "5":
        save_groups(groups)
        break
