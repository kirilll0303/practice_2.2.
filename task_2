import psutil #Библиотека win+r, "pip install psutil"
import time
import os

def clear_screen():
    """ """
    os.system ('cls' if os.name == 'nt' else 'clear')

def get_cpu_info():
    """INFO CPU"""
    cpu_percent = psutil.cpu_percent(interval = 3)
    
    cpu_per_core = psutil.cpu_percent(interval = 1, percpu = True)
    
    return cpu_percent, cpu_per_core

def get_ram_info():
    """INFO RAM"""
    memory = psutil.virtual_memory()

    total = memory.total / (1024**3)
    available = memory.available / (1024**3)
    used = memory.used / (1024**3)
    percent = memory.percent

    return {
        'total': round(total, 2),
        'available': round(available, 2),
        'used': round(used, 2),
        'percent': percent
    }

def get_disk_info():
    """INFO DISK"""
    disks = []
    for partition in psutil.disk_partitions():
        try:
            usage = psutil.disk_usage(partition.mountpoint)
            disk_info = {
                'device': partition.device,
                'mountpoint': partition.mountpoint,
                'total': usage.total / (1024**3), 
                'used': usage.used / (1024**3),
                'free': usage.free / (1024**3),
                'percent': usage.percent
            }
            disks.append(disk_info)
        except PermissionError:
            continue

    return disks

def draw_progress_bar (percent, width = 30, symbol = '='):
    filled = int(width * percent / 100)
    bar = symbol * filled + '-' * (width - filled)
    return f"[{bar}] {percent:.1f}%"

def main ():

    try:
        while True:
            clear_screen() #CLEAR MONITROR UPDATE 

            print ("_" * 50)
            print (f"TIME UPDATE: {time.strftime('%H:%M:%S')}")
            print ("-" * 50)

            print ("\n ___CPU___")
            cpu_percent, cpu_per_core = get_cpu_info()

            print(f"ALL: {draw_progress_bar(cpu_percent)}")

            for i, core in enumerate(cpu_per_core):
                print (f"Core {i}: {draw_progress_bar(core)}")

            print ("\n ___RAM___")
            ram = get_ram_info()

            
            print (f"ALL: {ram['total']} GB")
            print (f"USED: {ram['used']} GB")
            print (f"AVAILABLE: {ram['available']} GB")
            print (f"LOADING: {draw_progress_bar(ram['percent'])}")
            
            print("\n ___DISKS___:")
            disks = get_disk_info()
            
            for disk in disks:
                print (f"\nDISK {disk['device']} ({disk['mountpoint']}):")
                print (f"  ALL: {disk['total']:.1f} GB")
                print (f"  USED: {disk['used']:.1f} GB")
                print (f"  AVAILABLE: {disk['free']:.1f} GB")
                print (f"  LOADING: {draw_progress_bar(disk['percent'])}")

                print("\n" + "-" * 50)
                print("NEW A 10 SEC (Ctrl+C = EXIT)")

            time.sleep(10)
            
    except KeyboardInterrupt:
        print("\n\n PROGRAMM USED. BYE!")

if __name__ == "__main__":
    main()
