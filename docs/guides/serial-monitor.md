String input;
String getValue(String data, char separator, int index);

void setup() {
  Serial.begin(115200);
}

void loop() {
  if (Serial.available()) {
    input = Serial.readString();

    Serial.print("Nilai");
    Serial.print('\t');
    Serial.println(":" + getValue(input, ',', 0));
  }
}

String getValue(String data, char separator, int index) {
  int found = 0;
  int strIndex[] = {0, -1};
  int maxIndex = data.length() - 1;

  for (int i = 0; i <= maxIndex && found <= index; i++) {
    if (data.charAt(i) == separator || i == maxIndex) {
      found++;
      strIndex[0] = strIndex[1] + 1;
      strIndex[1] = (i == maxIndex) ? (i + 1) : i;
    }
  }

  return found > index ? data.substring(strIndex[0], strIndex[1]) : "";
}
