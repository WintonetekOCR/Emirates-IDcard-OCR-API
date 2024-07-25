# Emirates IDcard OCR API Calling 

## Introduction
Sinosecu Emirates IDcard Recognition OCR API support recognition Emirates national IDcard, including capture the head image from the template and save as JPG, PNG format, also can extract the text, like name, gender, date of birth, date of expiry, address and more... below is Java sample code to calling the reading result 

### JAVA SAMPLE CODE 

```

//dependency：okio-1.14.0,shiro-core-1.4.0,okhttp-3.11.0
import okhttp3.MultipartBody;
import okhttp3.OkHttpClient;
import okhttp3.Request;
import okhttp3.RequestBody;
import okhttp3.Response;
import org.apache.shiro.crypto.hash.Md5Hash;
import java.io.IOException;
import java.time.Instant;

public class Test {

    public static void main(String[] args) throws IOException {

        String key = "M***********g";
        String secret = "3***********6";

        long timestamp = Instant.now().toEpochMilli();
        String token = new Md5Hash(key + "+" + timestamp + "+" + secret).toString();

        RequestBody body = new MultipartBody.Builder().setType(MultipartBody.FORM)
                .addFormDataPart("img", "/9j")
                .addFormDataPart("key", key)
                .addFormDataPart("token", token)
                .addFormDataPart("timestamp", String.valueOf(timestamp))
                .addFormDataPart("typeId", "2")
                .build();
        Request request = new Request.Builder()
                .url("https://flyocr.com/api/recogliu.do")
                .method("POST", body)
                .build();
        OkHttpClient client = new OkHttpClient();
        Response response = client.newCall(request).execute();
        System.out.println(response.body().string());
    }
}
```
