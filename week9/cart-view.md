# 장바구니 보기

## Backdoor

```typescript
const { I } = inject();

const BACKDOOR_BASE_URL = process.env.BACKDOOR_BASE_URL
                          || 'http://localhost:3000/backdoor';

export = {
  setupDatabase() {
    I.amOnPage(`${BACKDOOR_BASE_URL}/setup-database`);
    I.see('OK');
  },
}
```

> 해당 URL은 테스트 환경에서만 사용하고 실제 서비스에 노출되면 안된다. 데이터베이스를 리셋하는 목적으로 사용.
> 해당 API는 MSW로 mocking한 것이 아닌 서버에서 제공하는 API.
