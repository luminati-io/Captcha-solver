# CAPTCHA Solver  

[![Promo](https://github.com/luminati-io/LinkedIn-Scraper/raw/main/Proxies%20and%20scrapers%20GitHub%20bonus%20banner.png)](https://brightdata.com/) 

Use [Bright Data's CAPTCHA Solver](https://brightdata.com/products/web-unlocker/captcha-solver) to effortlessly solve CAPTCHAs like reCAPTCHA, hCaptcha, PX Captcha, GeeTest, and more with user emulation, fingerprint management, and a powerful proxy infrastructure. 
Our CAPTCHA Solver is a built-in feature for our [Scraping Browser](https://brightdata.com/products/scraping-browser) and [Web Unlocker](https://brightdata.com/products/web-unlocker).



## Features  

- Rapid & automated CAPTCHA solving  
- Compatible with reCAPTCHA, hCaptcha, PX Captcha, GeeTest, SimpleCaptcha, and more  
- Intelligent user emulation and fingerprinting to bypass detection  
- Powered by an award-winning [proxy network with 100M+ IPs](https://brightdata.com/proxy-types)  
- Pay only for results with 99.9% uptime and 24/7 support  



## Why Choose CAPTCHA Solver  

- **Trusted by 20,000+ customers worldwide**  
- **Built for developers**  
  - AI-driven unlocking logic  
  - Automatic CAPTCHA solving and retries  
  - Built-in JavaScript rendering  
  - Easy integration with tools like Puppeteer, Playwright, and Selenium
 
 > **📚 Learn more about web scraping with:**
 >> [**Puppeteer**](https://brightdata.com/blog/how-tos/web-scraping-puppeteer)<br>
 >> [**Playwright**](https://brightdata.com/blog/how-tos/playwright-web-scraping)<br>
 >> [**Selenium**](https://brightdata.com/blog/how-tos/using-selenium-for-web-scraping)

- **Unmatched reliability**  
  - 99.9% success rates  
  - 4+ years of R&D and 80+ dedicated engineers  
  - Handles over 5.5 trillion data requests per year  



# How CAPTCHA Solver Works  

Bright Data’s CAPTCHA Solver is integrated into the **Scraping Browser** and **Web Unlocker** to **automatically solve CAPTCHAs** by default. You can:  

- Monitor the solving process in your code  
- Manually toggle CAPTCHA-solving behavior using Chrome DevTools Protocol (CDP) commands  
- Fully disable CAPTCHA solving if desired  



## **Automatic CAPTCHA Solving**  

Use the `Captcha.solve` command to detect and resolve CAPTCHAs automatically.

### Command Overview  

```javascript
Captcha.solve({
    detectTimeout?: number // Timeout for CAPTCHA detection in milliseconds  
    options?: CaptchaOptions[] // Configuration options for CAPTCHA solving  
}) : SolveResult
```

### Example: NodeJS (Puppeteer)

```javascript
const page = await browser.newPage();
const client = await page.target().createCDPSession();
await page.goto('https://site-with-captcha.com');

// Automatically solve CAPTCHA  
const { status } = await client.send('Captcha.solve', { detectTimeout: 30000 });   
console.log(`CAPTCHA solve status: ${status}`);
```

### Events Monitoring  

You can listen for specific CAPTCHA-solving events to handle advanced use cases:  

- **`Captcha.detected`**: CAPTCHA detected and solving has started  
- **`Captcha.solveFinished`**: CAPTCHA solved successfully  
- **`Captcha.solveFailed`**: CAPTCHA solving failed  
- **`Captcha.waitForSolve`**: Waiting for CAPTCHA solver to complete  

#### NodeJS Example - Listening for Events

```javascript
const client = await page.target().createCDPSession();   
await new Promise((resolve, reject) => {   
  client.on('Captcha.solveFinished', resolve);   
  client.on('Captcha.solveFailed', () => reject(new Error('CAPTCHA solving failed')));   
  setTimeout(reject, 300000, new Error('CAPTCHA solve timeout'));  
});
```

## Manual CAPTCHA Management

Need full control? Configure the behavior or disable solving entirely.

### Disable Automatic CAPTCHA Solving

```javascript
Captcha.setAutoSolve({  
  autoSolve: false // Disable CAPTCHA solving  
});
```

### Disable CAPTCHA Auto-Solve for Specific Types

```javascript
Captcha.setAutoSolve({  
  autoSolve: true,  
  options: [{  
    type: 'usercaptcha', // Disable auto-solving for this CAPTCHA type  
    disabled: true  
  }]  
});
```

### Manually Solve CAPTCHAs

```javascript
const page = await browser.newPage();  
const client = await page.target().createCDPSession();
await client.send('Captcha.setAutoSolve', { autoSolve: false });  
await page.goto('https://site-with-captcha.com');
const { status } = await client.send('Captcha.solve', { detectTimeout: 30000 });
console.log('CAPTCHA solve status:', status);
```

## Supported CAPTCHA Types  

Our solver supports a wide range of CAPTCHAs, including:  

## Supported CAPTCHA Types  

Our solver supports a wide range of CAPTCHAs, including:  

- [**reCAPTCHA**](https://brightdata.com/products/web-unlocker/captcha-solver/recaptcha)
- [**Click Captcha**](https://brightdata.com/products/web-unlocker/captcha-solver/click-captcha)
- [**hCaptcha**](https://brightdata.com/products/web-unlocker/captcha-solver/hcaptcha)
- [**PerimeterX**](https://brightdata.com/products/web-unlocker/captcha-solver/perimeterx)
- [**SimpleCaptcha**](https://brightdata.com/products/web-unlocker/captcha-solver/simplecaptcha)
- [**FunCaptcha**](https://brightdata.com/products/web-unlocker/captcha-solver/funcaptcha)
- [**Cloudflare Turnstile**](https://brightdata.com/products/web-unlocker/captcha-solver/cloudflare-turnstile)
- [**AWS WAF Captcha**](https://brightdata.com/products/web-unlocker/captcha-solver/aws-waf-captcha)
- [**GeeTest CAPTCHA**](https://brightdata.com/products/web-unlocker/captcha-solver/geetest-captcha)
- [**KeyCAPTCHA**](https://brightdata.com/products/web-unlocker/captcha-solver/keycaptcha)
- [**Puzzle CAPTCHA**](https://brightdata.com/products/web-unlocker/captcha-solver/puzzle-captcha)
- [**Yandex CAPTCHA**](https://brightdata.com/products/web-unlocker/captcha-solver/yandex-captcha)
- [**Image CAPTCHA**](https://brightdata.com/products/web-unlocker/captcha-solver/image-captcha)
- [**Text CAPTCHA**](https://brightdata.com/products/web-unlocker/captcha-solver/text-captcha)

  

## Advanced Customization  

Use advanced settings to fine-tune CAPTCHA-solving logic.  

### Example: Custom Options for Cloudflare Challenges  

```javascript
const cfOptions = {
  timeout: 40000,
  selector: '#challenge-body-text, .challenge-form',
  check_timeout: 300,
  success_selector: '#challenge-success[style*=inline]',
  wait_networkidle: { timeout: 500 }
};
```

## Pricing  

| **Plan**          | **Price (1K Results)** | **Monthly Cost** | **Description**                                                                   |  
|--------------------|------------------------|------------------|-----------------------------------------------------------------------------------|  
| **Pay-as-you-go**  | $1.50                 | No commitment    | Ideal for ad-hoc scraping needs.                                                 |  
| **Growth**         | $1.27                 | $499             | Tailored for scaling teams.                                                       |  
| **Business**       | $1.12                 | $999             | Suitable for large-scale scraping operations.                                     |  
| **Premium**        | $1.05                 | $1,999           | Advanced features with priority support for mission-critical operations.         |  
| **Enterprise**     | Custom Quote          | Contact Us       | Custom packages, premium SLA, dedicated Account Manager, SSO, and personalized solutions. |  

🚀 **SPECIAL OFFER**: Match your first deposit dollar-for-dollar up to **$500**!  


## Why Developers Love CAPTCHA Solver  

- **Easy Integration**: Works seamlessly with Puppeteer, Playwright, and Selenium.  
- **Advanced AI-Based Logic**: Handles retries, CAPTCHA solving, fingerprinting, IP rotation, and advanced headers automatically.  
- **Built-in Browser**: No need to manage external browsers for JavaScript rendering.  
- **Real-Time Insights**: Monitor network performance via a live dashboard.  
- **Unmatched Support**: 24/7 global customer support with new features added daily.  


## FAQ  

### **How Does CAPTCHA Solver Work?**  
CAPTCHA Solver detects, analyzes, and solves CAPTCHAs automatically using advanced AI-based logic.  

### **Can It Handle Multiple CAPTCHAs Simultaneously?**  
Yes, the solution scales to handle multiple CAPTCHA types concurrently.  

### **What Happens If CAPTCHA Solving Fails?**  
Retries are automatically attempted. If problems persist, contact our 24/7 support team to troubleshoot.  


**🌟 Get Started Today and Say Goodbye to CAPTCHAs!**  

**[Start Free Trial](https://brightdata.com/products/web-unlocker/captcha-solver)**  

