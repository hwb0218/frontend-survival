# Playwright

## Keyword

- E2E(End to End) Test
- Headless Chrome
- Puppeteer
- Playwright
- CodeceptJS

## 1. E2E(End to End) Test

사용자 관점에서 애플리케이션을 테스트하는 방법. 사용자가 서비스를 실제로 사용할 때 발생할 수 있는 시나리오를 재현하여 사용자 경험을 테스트하고 통과함으로써 서비스 무결성을 증명할 수 있게 된다.

---

## 2. Headless Chrome

Chrome을 GUI형태로 실행되는 것과는 달리, Headless Chrome은 CLI형태로 백그라운드에서 실행되는 브라우저를 말한다. UI로 보여줄 필요가 없는 웹 스크래핑, 테스트를 위한 용도로 사용된다.

---

## 3. Puppeteer

웹 브라우저 자동화 툴로 구글에서 개발한 Node.js 환경에서 실행되는 Headless Chrome과 Chromium을 제어하는 라이브러리다. Headless와 Non-Headless 모드를 on/off 할 수 있다.

**`Puppeteer 사용목적`**

1. 웹 페이지를 스크린샷하거나 PDF를 생성할 수 있다.
2. SPA 크롤링 가능 - page.goto()와 page.waitFor()를 사용해 SPA 페이지를 로드하고 필요한 요소들이 로드될 때까지 대기한다.
3. UI 테스트 자동화

**`웹 브라우저 자동화?`**

프로그래밍을 통해 웹 브라우저의 제어와 상호 작용을 자동화한 것. 직접 브라우저를 열고 웹 페이지를 방문해 상호 작용하지 않아도, 프로그램이 대신 자동으로 수행해주는 것 이다.

---

## 4. Playwright

MS에서 개발한 웹 브라우저 자동화 및 테스트를 위한 라이브러리.

**`Puppeteer가 있는데 왜 Playwright를 사용?`**

1. 다양한 브라우저 지원 - Puppeteer는 Chromium을 기반으로 하지만, Playwright는 여러 브라우저를 지원하기 때문에 크로스 브라우징 테스트에 적합하다.
2. 다양한 언어 지원 - JS뿐만 아니라 Python, TS를 지원한다.

---

## 5. CodeceptJS

E2E 테스트를 위한 사용자 친화적인 문법을 제공하는 Javascript 테스트 도구. 테스트 코드의 가독성을 높이며, 비개발자 입장에서도 편리하게 읽고 사용할 수 있다.

```javascript
Feature('기능 입력');

Scenario('Visit the home page', ({ I }) => {
  I.amOnPage('/');

  I.see('Hello, world!');
});

Scenario('Add a new post', ({ I }) => {
  I.amOnPage('/');

  I.dontSee('What time is it?');

  I.click('Add post!');

  I.waitForText('What time is it?');
});
```
