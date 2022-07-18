# [technical-assignment-week-5-faiz](https://github.com/impactbyte/iot-with-python-technical-assignments/tree/main/05-IoT-Hardware-2)
Repository for technical assignment week 5


## Pertanyaan & Jawaban

Menggunakan sebuah sensor ***selain sensor ultrasonic HC-SR04***, buatlah hal-hal berikut:

1. Wiring diagram untuk sensor tersebut menggunakan fritzing ( upload dalam MD files screenshot wiring diagram tersebut ) 
    <br>

   ![raspisensor](https://user-images.githubusercontent.com/67363618/179359093-4e69fe10-f958-49a1-9962-4df6982a595d.jpg)

2. Script sensor.py dan sebuah fungsi untuk mengambil data dari sensor tersebut
    ```python
    # sensor.py
    
    import Adafruit_DHT
    import time

    DHT_SENSOR = Adafruit_DHT.DHT11
    DHT_PIN = 4

    while True:
        humidity, temperature = Adafruit_DHT.read(DHT_SENSOR, DHT_PIN)

    if humidity is not None and temperature is not None:
        print("Temp={0:0.1f}*C  Humidity={1:0.1f}%".format(temperature, humidity))
    else:
        print("Failed to retrieve data from humidity sensor")
    time.sleep(1)
    ```

3. Sebuah script utama [main.py](http://main.py) yang terdiri dari sebuah logic sederhana yang menjawab sebuah use case sederhana ( jelaskan use case tersebut dalam MD files! )
    ```python
    # main.py
    
    import Adafruit_DHT
    import time
    import RPi.GPIO as GPIO  
    
   SENSOR = Adafruit_DHT.DHT11
   PIN = 4
    
    try:
        while True:
            lembab, suhu = Adafruit_DHT.read(SENSOR, PIN)

            if lembab is not None and suhu is not None:
                print("Suhu={0:0.1f}*C  Kelembaban={1:0.1f}%".format(suhu, lembab))

                # menambah logic untuk print suatu keadaan suhu jika: suhu kurang dari || lebih dari sekian temperatur
                if suhu <= 34 and suhu >= 15:
                    print("Suhu normal")
                elif suhu >= 34 and suhu <= 45:
                    print("Suhu panas")
                elif suhu <= 15 and suhu >= -15 :
                    print("Suhu dingin")
                else:
                    print("Suhu tidak normal, membahayakan")

            else:
                print("Tidak bisa membaca data dari sensor")
            time.sleep(1)
        
        
    # Menghentikan program dengan CTRL + C
    except KeyboardInterrupt:
        print("Sensor dihentikan")
    ```
4. (Optional) Ambil sekitar 5 - 10 sample data dan tampilkan dalam sebuah grafik matplotlib dan screenshot hasil tersebut dan upload pada MD files.
