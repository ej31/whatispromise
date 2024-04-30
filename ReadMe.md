```html
<!doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>사용자 정보 조회 앱</title>
</head>
<body>
<h1>사용자 정보 조회</h1>
<input type="number" id="userIdInput" placeholder="사용자 ID 입력">
<button onclick="fetchData()">사용자 정보 가져오기</button>
<div id="userInfo"></div>
<script>
    function fetchData(userId) {
        // fetch 함수를 사용하여 JSONPlaceholder에서 사용자 데이터를 가져옴
        return fetch(`https://jsonplaceholder.typicode.com/users/${userId}`) // 3번째 줄`
                .then((response) => {
                    if (!response.ok) {
                        throw new Error("Network response was not ok");
                    }
                    return response.json(); // 6번째 줄
                })
                .then((data) => {
                    // 사용자 정보를 HTML 요소에 표시
                    document.getElementById('userInfo').innerText = JSON.stringify(data, null, 2);
                })
                .catch((error) => {
                    console.error("Fetch error:", error); // 9번째 줄
                });
    }

    function fetchData() {
        // 입력 필드에서 사용자 ID를 가져옴
        const userId = document.getElementById('userIdInput').value;
        // 데이터 로드 호출
        fetchData(userId);
    }

</script>
</body>
</html>
```

```mermaid
sequenceDiagram
    participant MN as 🥷 메인 닌자
    participant CS as 🥷 분신: fetchData
    participant NW as 네트워크
    participant JS as JSON 파싱

    MN->>+CS: 분신술 발동 (fetchData 호출)
    Note right of MN: 🥷 메인 닌자가 분신의 결과를 기다림
    CS->>+NW: 은밀한 데이터 요청 (fetch)
    Note over NW: 네트워크가 응답을 처리함
    NW-->>-CS: 응답 도착
    CS->>+JS: 응답을 JSON으로 변환
    JS-->>-CS: JSON 데이터 준비 완료
    CS-->>-MN: 데이터 반환
    Note right of MN: 🥷 메인 닌자가 응답을 받고 활동 재개
    MN->>MN: 데이터 처리 또는 오류 대응
    Note over MN: 결과를 사용하거나 오류를 로깅
```
## 참고 사항
- 다이어그램에서 세로 라인 중 두꺼운 부분은 호출한 부분에서 응답을 기다린다는 뜻입니다. :ninja:
