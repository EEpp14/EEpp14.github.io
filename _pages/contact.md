---
layout: page
title: Contact
permalink: /contact/
description: I care about my readers' opinions. Please leave a note or just say hello.
---

### You can reach me with the form below


<form action="https://formspree.io/{{site.data.main.email}}" method="POST">
  <div class="form-group">
    <label for="email">Email address</label>
    <input type="email" name="email" class="form-control" placeholder="Enter email">
  </div>
  <div class="form-group">
    <label for="message">Example textarea</label>
    <textarea class="form-control" name="content" id="" rows="3" placeholder="Enter your message"></textarea>
  </div>
  <input type="hidden" name="_next" value="{{site.url}}{{page.url}}">
  <input type="hidden" name="_subject" value="New Contact Form Submission">
  <input type="text" name="_gotcha" style="display:none">
  <button type="submit" class="btn btn-success">Submit</button>
</form>

<br>
<br>