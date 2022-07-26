```Processing
void setup() {
  size(300, 300);

  String str = "_-.";
  String c = "3";
  println(str);

if (char_inString(c,str)){
println(1);
}
}

void draw() {
}

boolean char_inString(String subset, String ori) {
  for (int i =0; i< ori.length(); i++) {
    String  curr = ori.substring(i,i+1);
    println("curr:"+curr);
    if (subset.equals(curr)) {
      return true;
    }
  }
  return false;
}


```
