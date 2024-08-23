<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Reset Password</title>
</head>
<body>
    <h1>Reset Your Password</h1>
    <form id="resetPasswordForm">
        <input type="hidden" id="email" name="email" />
        <input type="hidden" id="token" name="token" />
        
        <label for="newPassword">New Password:</label>
        <input type="password" id="newPassword" name="newPassword" required />

        <label for="confirmPassword">Confirm Password:</label>
        <input type="password" id="confirmPassword" name="confirmPassword" required />

        <button type="submit">Reset Password</button>
    </form>

    <script>
        document.addEventListener('DOMContentLoaded', function () {
            const urlParams = new URLSearchParams(window.location.search);
            document.getElementById('email').value = urlParams.get('email');
            document.getElementById('token').value = urlParams.get('token');
        });

        document.getElementById('resetPasswordForm').addEventListener('submit', async function (event) {
            event.preventDefault();
            
            const email = document.getElementById('email').value;
            const token = document.getElementById('token').value;
            const newPassword = document.getElementById('newPassword').value;
            const confirmPassword = document.getElementById('confirmPassword').value;

            if (newPassword !== confirmPassword) {
                alert('Passwords do not match!');
                return;
            }

            const response = await fetch('https://your-backend.com/api/auth/reset-password', {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify({ email, token, newPassword })
            });

            if (response.ok) {
                alert('Password reset successfully!');
                window.location.href = 'https://your-website.com/login';
            } else {
                alert('Failed to reset password. Please try again.');
            }
        });
    </script>
</body>
</html>
