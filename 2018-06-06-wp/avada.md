# avada

## add text next logo image

* style.css
* Avada > Theme Options > Custom CSS
* ```css
  /* remove logo image
  .fusion-logo img {
  display: none !important;
  }
  */
  .fusion-logo a:before {
  content: “글짜글짜” !important;
  line-height: 48px !important;
  font-size: 36px !important;
  color: black!important;
  }
  ```

## 블로그 목록이나 아카이브(카테고리, 태그 등) 목록에서 블로그 링크와 이미지 줌 아이콘 없애기

* AVADA > 테마 옵션을 누르고 Extra > Featured Image Rollover 옵션 페이지로 이동
*   Image Rollover Link Icon(1)을 Off로 설정하면 링크 모양의 아이콘이 사라집니다.&#x20;

    그리고 Image Rollover Zoom Icon(2)을 비활성화하면 돋보기 모양의 아이콘(이미지 확대 아이콘)이 표시되지 않습니다.

\*번역: Poedit 프로그램이나 Loco Translate 같은 플러그인을 사용

\*\* with inspect, find element class:

## 아바다 테마에서 포맷 박스 아이콘(펜 모양 아이콘) 숨기기

[https://www.wordnpress.com/wordpress/hide-pen-icon-in-avada-theme-in-wordpress/](https://www.wordnpress.com/wordpress/hide-pen-icon-in-avada-theme-in-wordpress/)

```css
.home .fusion-format-box {
display: none;
}
```

## click image show big image

click image modal ? Image Lightbox - this option allows you display the image in a lightbox. with same image ? Lightbox Image - this option lets you upload a different image to display on the lightbox.

image lightbox? with image max width
