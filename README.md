🚀 Ví dụ sử dụng
Tạo profile và điều khiển qua Local API
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
        Console.WriteLine("Debugger Address: " + debuggerAddress);

        // Lấy cookies
        JArray cookies = api.GetCookies(profileId);
        Console.WriteLine("Cookies: " + cookies.ToString());

        // Stop profile
        api.StopProfileLocal(profileId);

        // Xoá profile nếu cần
        api.DeleteProfile(profileId);
    }
}

🌐 Sử dụng với Selenium WebDriver

Bạn có thể kết nối Selenium WebDriver tới browser GoLogin đang chạy
bằng DebuggerAddress từ StartProfileLocal.

using GoLoginNet;
using OpenQA.Selenium;
using OpenQA.Selenium.Chrome;
using System;

class Program
{
    static void Main()
    {
        var apiKey = "YOUR_GoLogin_API_KEY";
        var api = new GoLoginApi(apiKey);

        // 1. Tạo profile mới (hoặc dùng profile đã có)
        var profileId = api.CreateProfile("TestProfile", "", "", "");
        Console.WriteLine("Profile ID: " + profileId);

        // 2. Start profile qua Local API
        var debuggerAddress = api.StartProfileLocal(profileId);
        Console.WriteLine("Debugger Address: " + debuggerAddress);

        // 3. Kết nối Selenium tới GoLogin browser
        var chromeOptions = new ChromeOptions();
        chromeOptions.DebuggerAddress = debuggerAddress;

        var driver = new ChromeDriver(chromeOptions);

        // 4. Điều khiển browser bình thường
        driver.Navigate().GoToUrl("https://whoer.net/");
        Console.WriteLine("Tiêu đề trang: " + driver.Title);

        // 5. Đóng browser và stop profile
        driver.Quit();
        api.StopProfileLocal(profileId);

        // Xoá profile nếu cần
        api.DeleteProfile(profileId);
    }
}

🔧 Tính năng chính

Quản lý extension: thêm/xoá Chrome extension trong profile

Quản lý cookies: import/export cookies qua Cloud API

Profile API: tạo, xoá, start/stop profile qua Cloud hoặc Local API

Proxy support: hỗ trợ HTTP proxy (host, port, username, password)

🛠️ Debug vs Release

Debug build:

Dùng để phát triển và test

Xuất file bin\Debug\GoLoginNet.dll

Bao gồm file .pdb để debug

Release build:

Dùng để deploy hoặc publish NuGet

Xuất file bin\Release\GoLoginNet.dll

Nhẹ và tối ưu hơn

Chọn chế độ build ở thanh công cụ Visual Studio (Debug / Release).

📄 Giấy phép

MIT License — được phép sử dụng tự do cho mục đích cá nhân hoặc thương mại.
