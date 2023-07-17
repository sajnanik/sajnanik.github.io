---
title: "Troubleshooting PrestaShop Checkout Issue After Updating to 1.7.x.x"
date: 2023-01-01 T19:34:30-04:00
categories:
  - blog
tags:
  - IT Helpdesk
  - Tutorials
  - Prestashop
---

Hello everyone! Today, I want to share a recent issue I encountered with PrestaShop after updating to version 1.7.x.x. It was quite frustrating, but I managed to find a solution, and I hope this post helps others facing the same problem.

## The Scenario

After updating my PrestaShop store to any version in the 1.7.x.x series, I noticed that some customers were unable to proceed past the address input field during checkout. The problem was that once the customer entered their address details, the form kept reloading and didn't progress to the carrier selection or payment options.

## My Assumptions

After some research and digging into the code changes between versions, I assumed that the issue was related to the address format. It seemed that some new fields were introduced in the 1.7.x.x update, which the theme I was using wasn't formatted to handle properly. While customers filled all the required fields on the front end, the backend might still have been expecting additional fields, causing the form to keep reloading.

Additionally, there could have been changes in the formatting of certain address fields that could have caused the issue. Whatever the cause, I was determined to find a solution and make the checkout process smooth again for my customers.
The Solution

After some trial and error, I found a simple yet effective fix. Here's what you need to do:

1. Navigate to International > Countries: In the PrestaShop admin panel, go to the "International" tab and select "Countries" from the dropdown.

2. Select the Country to Edit: Identify the country where the checkout issue is occurring and click on it to edit its settings.

3. Address Format: In the middle of the page, you'll see the "Address format" section, which is crucial for our fix.

4. Clear the Format: Click on the "Clear format" button to remove any custom formatting that might be causing conflicts.

5. Use the Default Format: Once you've cleared the format, click on the "Use the default format" button. This will revert the address format to the default settings.

6. Save Changes: Save the changes you made for that specific country.

7. Repeat for Other Countries: If the issue is not limited to just one country, repeat the same process for all the countries affected by the checkout problem.

8. Clear Cache: After making changes to the address formats, it's essential to clear the PrestaShop cache. Go to the "Advanced Parameters" tab in the admin panel and select "Performance." Click on the "Clear cache" button to ensure the changes take effect.

![PrestaShop Checkout Issue](assets/images/prestashop-checkout-1.7-issue.png)


## Conclusion

After implementing the above steps for all the affected countries and clearing the cache, I was thrilled to see that the checkout process was working flawlessly again. It turned out that the formatting changes were causing the form to reload continuously, but now the issue is resolved.

However, it's worth noting that whenever you update PrestaShop in the future (which fortunately doesn't happen too often), you may need to reapply these changes. Keep an eye on any updates and be prepared to carry out this solution if the issue resurfaces.

I hope this post helps others who encounter a similar problem. Happy selling, and may your PrestaShop store run smoothly! If you have any questions or alternative solutions, feel free to share them in the comments.