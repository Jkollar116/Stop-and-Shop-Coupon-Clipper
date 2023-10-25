
# Stop and Shop Coupon Clipper

Easily add all available coupons to your Stop and Shop account with this bookmarklet!

## How to Use:

1. Copy the code below.
2. Create a new bookmark in your browser.
3. Instead of entering a URL, paste the copied code.
4. Name the bookmark something like "Clip Stop & Shop Coupons".
5. Whenever you're on the Stop & Shop coupons page, click the bookmarklet to clip all available coupons.

<pre>
javascript:(function run() {const delayLoop = (fn, delay) => {return (x, i) => {setTimeout(() => {fn(x);}, i * delay);};};const fireEvent = (element, type) => {const event = new MouseEvent(type, {'view': window,'bubbles': true,'cancelable': true});element.dispatchEvent(event);};const isVisible = (elem) => {const style = window.getComputedStyle(elem);return style.display !== 'none' && style.visibility !== 'hidden' && elem.offsetHeight !== 0;};let previousCouponCount = 0;const interval = setInterval(() => {const showMoreButton = document.querySelector('button#show-more');if (showMoreButton && isVisible(showMoreButton)) {fireEvent(showMoreButton, 'click');const currentCouponCount = document.querySelectorAll('button > div > div > svg.vector-icon-stroke--coupon').length;if (currentCouponCount === previousCouponCount) {clearInterval(interval);clipCoupons();}previousCouponCount = currentCouponCount;} else {clearInterval(interval);clipCoupons();}}, 3000);function clipCoupons() {const coupons = [...document.querySelectorAll('button > div > div > svg.vector-icon-stroke--coupon')].map(svg => svg.closest('button')).filter(isVisible);const totalCoupons = coupons.length;let couponsLeft = totalCoupons;coupons.forEach(delayLoop((e) => {fireEvent(e, 'click');console.log(%60Coupons left: ${couponsLeft}%60);couponsLeft = couponsLeft - 1;}, 150));}})();
</pre>
