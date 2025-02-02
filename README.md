The `esc_*` functions in WordPress are used to sanitize and escape data before outputting it to the browser. This helps protect your site from security vulnerabilities such as Cross-Site Scripting (XSS) attacks.

### 1. **`esc_html()`**

- **Purpose**: Escapes HTML to prevent rendering HTML tags, ensuring that any HTML entities are properly encoded.

#### Example:

```php
<?php
$input = '<strong>Hello World</strong>';

// Without esc_html
echo $input; // Outputs: <strong>Hello World</strong> (This will render the text as bold)

// With esc_html
echo esc_html($input); // Outputs: &lt;strong&gt;Hello World&lt;/strong&gt; (This will display the tags as text)
?>
```

### 2. **`esc_attr()`**

- **Purpose**: Escapes HTML attributes. This is important when you are dynamically inserting data into attributes like `href`, `src`, `title`, etc.

#### Example:

```php
<?php
$input = 'Hello "World"';

// Without esc_attr
echo '<a href="example.com" title="' . $input . '">Link</a>';
// Outputs: <a href="example.com" title="Hello "World"">Link</a> (This can break the attribute due to the unescaped quotes)

// With esc_attr
echo '<a href="example.com" title="' . esc_attr($input) . '">Link</a>';
// Outputs: <a href="example.com" title="Hello &quot;World&quot;">Link</a> (The quotes are safely escaped)
?>
```

### 3. **`esc_url()`**

- **Purpose**: Escapes URLs to ensure they are safe to use in HTML attributes like `href` or `src`.

#### Example:

```php
<?php
$url = 'http://example.com/?name=<script>alert("XSS")</script>';

// Without esc_url
echo '<a href="' . $url . '">Click here</a>';
// Outputs: <a href="http://example.com/?name=<script>alert("XSS")</script>">Click here</a>
// This could potentially execute the JavaScript in the URL.

// With esc_url
echo '<a href="' . esc_url($url) . '">Click here</a>';
// Outputs: <a href="http://example.com/?name=%3Cscript%3Ealert%28%22XSS%22%29%3C/script%3E">Click here</a>
// The script tags are escaped and won't execute.
?>
```

### 4. **`esc_js()`**

- **Purpose**: Escapes a string for safe use within JavaScript. This is useful when you’re outputting data within inline JavaScript.

#### Example:

```php
<?php
$input = 'Hello "World"';

// Without esc_js
echo '<script>alert("' . $input . '");</script>';
// Outputs: <script>alert("Hello "World"");</script>
// This can break the JavaScript code due to unescaped quotes.

// With esc_js
echo '<script>alert("' . esc_js($input) . '");</script>';
// Outputs: <script>alert("Hello \"World\"");</script>
// The quotes are safely escaped, keeping the JavaScript intact.
?>
```

### 5. **`esc_textarea()`**

- **Purpose**: Escapes content to be safely used within a `<textarea>` element, ensuring that HTML entities and new lines are properly encoded.

#### Example:

```php
<?php
$input = "Hello <strong>World</strong>\nNew line here.";

// Without esc_textarea
echo '<textarea>' . $input . '</textarea>';
// Outputs: <textarea>Hello <strong>World</strong>
// New line here.</textarea>
// This could cause issues if the content contains HTML tags or special characters.

// With esc_textarea
echo '<textarea>' . esc_textarea($input) . '</textarea>';
// Outputs: <textarea>Hello &lt;strong&gt;World&lt;/strong&gt;&#10;New line here.</textarea>
// The HTML tags and new lines are safely escaped.
?>
```

### Summary:
- **`esc_html()`**: Escapes HTML content, converting special characters to HTML entities.
- **`esc_attr()`**: Escapes content for safe use in HTML attributes.
- **`esc_url()`**: Ensures URLs are safe to use in attributes.
- **`esc_js()`**: Escapes content for safe use within JavaScript.
- **`esc_textarea()`**: Escapes content for safe use within `<textarea>` elements.

These functions are essential for securely outputting dynamic data in WordPress, helping to prevent potential security issues and ensuring that the content is displayed as intended.
