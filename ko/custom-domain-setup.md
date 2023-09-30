---
description: Enterprise 플랜 사용자를 위한 커스텀 도메인 초대링크 설정 방법을 안내합니다.
---

# 👩💻 커스텀 도메인 설정

기본적으로는 `https://nguard.xyz/invite/[something]` 와 같이 생긴 초대 링크 URL이 생성됩니다.\
그러나 Enterprise 플랜을 사용하시는 경우 소유하고 계신 도메인에 초대 링크를 설정하실 수 있습니다.

커스텀 도메인을 설정하기 위해서는 아래 단계를 진행해 주세요.\
이 섹션의 단계를 진행하는 동안 문제가 발생하면 NGuard Console 우측 하단 채널톡을 통해 문의해 주세요.

## 1. 도메인 고르기

오직 `하위 도메인`만 설정할 수 있습니다. `Apex 도메인`은 사용할 수 없습니다.

다음은 선택할 수 있는 것과 없는 것의 몇 가지 예입니다.

| 도메인 타입      | 예시                                                                                                              | 지원 여부 |
| ----------- | --------------------------------------------------------------------------------------------------------------- | :---: |
| Apex 도메인    | `example.com`                                                                                                   |   ❌   |
| `www` 서브도메인 | `www.example.com`                                                                                               |   ✅   |
| 커스텀 서브도메인   | <p><code>discord.example.com</code><br><code>invite.example.com</code><br><code>anything.example.com</code></p> |   ✅   |

## 2. 커스텀 도메인 설정하기

NGuard Console에서 초대링크 설정에 들어가면, 커스텀 도메인을 설정할 수 있는 메뉴를 확인할 수 있습니다.

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

커스텀 초대링크 토글을 눌러 활성화 하면, 아래와 같은 화면을 볼 수 있습니다:

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

이제 '도메인 설정' 란에 설정하려는 커스텀 도메인을 입력합니다.\
(아직 저장하면 안됩니다.)

## 3. DNS 설정하기

DNS 설정은 NGuard Console이 아닌, 커스텀 도메인의 DNS 공급자에서 진행해야 합니다.

**이 단계는 커스텀 도메인으로 초대링크를 사용하기 위해서 매우 중요합니다.**

### CNAME 레코드 설정하기

각 입력해야 하는 정보와 DNS 설정은 DNS 공급자마다 다를 수 있지만 여기서는 가장 일반적인 옵션을 다루었습니다.\
확실하지 않은 경우 DNS 공급자에게 문의하세요.

* **유형**은 만들려는 DNS 레코드의 종류입니다. 여기에서 **CNAME**을 선택해야 합니다.
* **이름** 또는 **DNS 엔트리**는 하위 도메인을 입력하는 공간입니다.\
  입력했던 커스텀 도메인 전체를 입력해야 할 수도 있고, Apex 도메인 앞 부분만 입력해야 할 수도 있습니다.\
  어떤 것을 사용해야 할지 잘 모르겠다면 DNS 공급자에게 문의하세요.
* **대상** 또는 **값**은 하위 도메인이 가리켜야 하는 위치입니다.
* **TTL (Time-to-Live)**는 **자동** 혹은 43200초(12시간) 내지는 86400초(24시간)로 설정하는 것이 좋습니다.

다음은 Cloudflare에서 올바르게 설정된 예입니다.

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

#### Cloudflare를 사용하고 계신가요?

Cloudflare를 DNS 공급자로 사용하고 계신 경우, **주황색 구름 (Proxied)** 로 설정하였는지 확인하시고,\
NGuard Console에서 **SSL 설정을 꺼주세요**.

원하신다면, **회색 구름 (DNS-only)** 로 설정하고 **SSL 설정을 켜실 수 있으나**, 추천드리지 않습니다.\
이는 보안에 취약해 질 수 있기 때문입니다. 주황색 구름이 아닌 경우 다른 사용자가 서비스를 남용하거나 DDoS 공격을 진행할 수 있습니다.

### 변경 사항 적용 기다리기

앞서 언급한 TTL(Time To Live) 필드를 기억하시나요?\
DNS 레코드는 일정 기간 동안 캐시됩니다. 이는 일반적으로 자주 변경되지 않기 때문에 성능상의 이유로 매우 좋습니다.

그러나 변경이 발생되었을 때 다시 캐시되기 까지 약간의 시간이 소요될 수 있습니다.\
대부분의 경우 한 시간 정도 시간이 소요됩니다. 때로는 모든 것이 조금 더 빨리 업데이트될 수도 있고, 더 오래 걸릴 수도 있습니다.

[WhatsMyDNS ](https://www.whatsmydns.net/#CNAME)라는 사이트에서 설정한 DNS가 적용되고 있는지 확인할 수 있습니다.\
이 사이트 상단에 설정하신 커스텀 도메인의 전체를 입력하고, Search를 눌러주세요.

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

DNS가 아직 적용되지 않은 경우 아래와 같이 표시됩니다.

<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

DNS가 성공적으로 적용된 경우 아래와 같이 표시됩니다.

<figure><img src="../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

DNS가 성공적으로 적용된 것이 확인 되었다면, 다음 단계로 진행할 수 있습니다.\
**SSL 설정이 켜져있는 경우, DNS가 성공적으로 적용되기 전에 다음 단계로 진행하지 마세요.**

## 4. 설정 완료하기

다시 2단계에서의 NGuard Console로 돌아갑니다.

<figure><img src="../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

이제 저장하기 버튼을 눌러 저장해 주세요.

<figure><img src="../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

'확인' 버튼을 눌러 저장해 주세요.

**🎉 커스텀 도메인 설정이 완료되었습니다! 설정하신 커스텀 도메인으로 접속해 보세요!**
