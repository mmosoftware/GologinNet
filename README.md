
# GoLoginNet

**GoLoginNet** là một thư viện C# wrapper cho [GoLogin API](https://gologin.com/), hỗ trợ quản lý profile, cookie, extension và khởi chạy browser qua cả Cloud API và Local API.

> Hỗ trợ: **.NET Framework 4.5** (và có thể sử dụng trên .NET Core/.NET 6+ với chỉnh sửa nhỏ).

---

## 📦 Cài đặt

### Từ NuGet
```powershell
Install-Package GoLoginNet

Hoặc tham chiếu DLL trực tiếp

Build project ở chế độ Release

Lấy file bin\Release\GoLoginNet.dll

Add Reference vào project của bạn

🚀 Sử dụng

Ví dụ khởi tạo API, tạo profile và chạy bằng Local API:



using GoLoginNet;
using Newtonsoft.Json.Linq;
using System;

class Program
{
    static void Main()
    {
        var apiKey = "YOUR_GoLogin_API_KEY";
        var api = new GoLoginApi(apiKey);

        // Tạo profile mới
        var profileId = api.CreateProfile("TestProfile", "", "", "");
        Console.WriteLine("Profile created: " + profileId);

        // Start profile qua Local API và lấy DebuggerAddress
        var debuggerAddress = api.StartProfileLocal(profileId);
        Console.WriteLine("Debugger address: " + debuggerAddress);

        // Lấy cookies từ profile
        JArray cookies = api.GetCookies(profileId);
        Console.WriteLine("Cookies: " + cookies.ToString());

        // Stop profile
        api.StopProfileLocal(profileId);

        // Xoá profile nếu cần
        api.DeleteProfile(profileId);
    }
}

🔧 Các tính năng chính

Quản lý extension: Thêm/xóa Chrome extension vào profile

Quản lý cookies: Import/Export cookies qua Cloud API

Profile API: Tạo, xoá, start/stop profile qua Cloud API hoặc Local API

Proxy support: Hỗ trợ HTTP proxy (host, port, user, pass)

📄 License

MIT License — thoải mái sử dụng cho mục đích cá nhân hoặc thương mại.
