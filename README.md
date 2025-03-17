make_minimum_required(VERSION 3.10)

project(DartErkennung)

set(CMAKE_CXX_STANDARD 17)

# OpenCV einbinden
find_package(OpenCV REQUIRED)
include_directories(${OpenCV_INCLUDE_DIRS})

# Füge deine Quellcode-Dateien hinzu
add_executable(DartErkennung main.cpp)

# OpenCV-Bibliotheken verlinken
target_link_libraries(DartErkennung ${OpenCV_LIBS})
rtsp://admin:100Mebess!!@192.168.2.186:554/h264Preview_01_main
import cv2

# RTSP-Stream-URL
rtsp_url = "rtsp://admin:100Mebess!!@192.168.2.186:554/h264Preview_01_main"

# Verbindung zur Kamera herstellen
cap = cv2.VideoCapture(rtsp_url)

if not cap.isOpened():
    print("Fehler: Kamera-Stream konnte nicht geöffnet werden.")
    exit()

while True:
    ret, frame = cap.read()
    if not ret:
        print("Fehler beim Lesen des Frames.")
        break

    # Zeige das Bild an
    cv2.imshow("Dartboard Stream", frame)

    # Beenden mit 'q'
    if cv2.waitKey(1) & 0xFF == ord('q'):
        break

cap.release()
cv2.destroyAllWindows()
name: Build C++ EXE

on: [push, pull_request]

jobs:
  build:
    runs-on: windows-latest
    steps:
      - name: Checkout Repository
        uses: actions/checkout@v3

      - name: Install MinGW
        run: choco install mingw --yes

      - name: Compile C++ Code
        run: g++ -o mein_programm.exe mein_programm.cpp

      - name: Upload EXE Artifact
        uses: actions/upload-artifact@v3
        with:
          name: meine-exe
          path: mein_programm.exe
