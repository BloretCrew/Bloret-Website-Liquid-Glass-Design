# Bloret Website Liquid Glass Design


## 简介

Bloret 网页界面（BBBS、Bloret PassPort、ChaFuWang 以及 Bloret Launcher 授权等界面）的统一玻璃设计规范

## 设计思路

为了提高代码的可维护性、可读性和复用性，我们将原本分散在 `web.py` 文件中各个 HTML 生成方法（如 `generate_success_page`、`generate_plugin_confirmation_page` 和 `generate_installing_page`）内部的内联 CSS 样式进行了提取。

**主要设计原则：**

1.  **分离关注点 (Separation of Concerns):** 将 HTML 结构、CSS 样式和 JavaScript 行为分离，使代码结构更清晰，便于不同职责的开发人员协作。
2.  **提高可维护性:** 当需要修改样式时，只需编辑一个独立的 CSS 文件，而不是在多个 Python 方法中查找和修改内联样式。
3.  **减少冗余:** 多个页面共享相同的基本样式，通过外部 CSS 文件可以避免重复定义这些样式。
4.  **优化加载性能 (潜在):** 浏览器可以缓存外部 CSS 文件，减少重复下载，从而可能提高页面加载速度。

通过将所有相关样式合并到一个外部 CSS 文件中，并在 HTML 模板中通过 `<link rel="stylesheet" href="/index.css">` 引入，我们实现了样式的集中管理和复用。

## 合并后的 CSS 样式

```css
body {
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    margin: 0;
    background-image: url('https://api.imlazy.ink/img');
    background-size: cover;
    background-position: center;
    background-repeat: no-repeat;
}
.container {
    background: rgba(255, 255, 255, 0.35);
    border-radius: 18px;
    box-shadow: 0 8px 32px rgba(31, 38, 135, 0.18), 0 1.5px 8px 0 rgba(255, 255, 255, 0.25) inset;
    border: 1.5px solid rgba(255, 255, 255, 0.45);
    padding: 40px;
    text-align: center;
    backdrop-filter: blur(18px) saturate(180%);
    -webkit-backdrop-filter: blur(18px) saturate(180%);
    max-width: 500px;
    width: 80%;
}
h1 {
    color: white;
    font-weight: 500;
    margin-bottom: 20px;
    font-size: 28px;
}
p {
    font-size: 18px;
    color: rgba(255, 255, 255, 0.95);
    line-height: 1.6;
    margin: 10px 0;
}
.icon {
    font-size: 48px;
    margin-bottom: 20px;
    color: white;
}
.warning {
    color: #ffcc00;
    font-weight: bold;
    margin: 20px 0;
    padding: 15px;
    background: rgba(255, 204, 0, 0.2);
    border-radius: 10px;
    font-size: 16px;
}
.plugin-info {
    background: rgba(255, 255, 255, 0.2);
    border-radius: 10px;
    padding: 15px;
    margin: 20px 0;
    text-align: left;
}
.plugin-info div {
    margin: 10px 0;
}
.btn {
    background-color: #4CAF50;
    color: white;
    padding: 12px 24px;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    font-size: 16px;
    margin: 10px;
}
.btn.cancel {
    background-color: #f44336;
}
.btn:hover {
    opacity: 0.9;
}
.spinner {
    border: 4px solid rgba(255, 255, 255, 0.3);
    border-radius: 50%;
    border-top: 4px solid white;
    width: 40px;
    height: 40px;
    -webkit-animation: spin 1s linear infinite;
    animation: spin 1s linear infinite;
    margin: 20px auto;
}
@-webkit-keyframes spin {
    0% { -webkit-transform: rotate(0deg); }
    100% { -webkit-transform: rotate(360deg); }
}
@keyframes spin {
    0% { transform: rotate(0deg); }
    100% { transform: rotate(360deg); }
}
@keyframes fadeIn {
    from { opacity: 0; transform: translateY(20px); }
    to { opacity: 1; transform: translateY(0); }
}
```
