
## Responsible Use

BloodServer is a tool for professional penetration testers and should only be used in environments where you have explicit permission. Misuse of this tool could lead to security vulnerabilities if deployed in inappropriate settings.

## Future Improvements

I'm constantly working on improving BloodServer. Future updates may include:

- More robust authentication methods
- Improved logging and monitoring
- File integrity checks
- Automatic cleanup of transferred files

## Conclusion

BloodServer aims to fill a niche need for penetration testers who require a quick, secure file transfer solution during engagements. While it's a powerful tool in the right hands, always remember the importance of responsible use and adherence to security best practices.

Feel free to contribute to the project or report issues on [GitHub link].

Stay secure, and happy testing!# BloodServer: Secure File Transfer Server

BloodServer is a simple yet secure file transfer server implemented in Python by bloodstiller. It supports both HTTP and HTTPS protocols, basic authentication, and can be easily configured through command-line arguments.

## Features

- HTTP and HTTPS support
- Basic authentication
- Configurable port, username, and password
- File upload functionality
- Graceful shutdown option
- Logging of server activities

## Requirements

- Python 3.6+
- OpenSSL (for HTTPS support)

## Installation

1. Clone this repository:
   ```
   git clone https://github.com/bloodstiller/bloodserver.git
   cd bloodserver
   ```

2. (Optional) Create a virtual environment:
   ```
   python -m venv venv
   source venv/bin/activate  # On Windows use `venv\Scripts\activate`
   ```

3. No additional dependencies are required as BloodServer uses Python standard library modules.

## Usage

### Starting the Server

Run the server using the following command:

```
python bloodserver.py [options]
```

Options:
- `-p PORT, --port PORT`: Port to run the server on (default: 9999)
- `--https`: Enable HTTPS (requires `server.pem` file)
- `-u USERNAME, --username USERNAME`: Set the username for authentication (default: admin)
- `--password PASSWORD`: Set the password for authentication (if not set, a random password will be generated)

Example:
```
python bloodserver.py -p 8080 -u bloodstiller --password bl00dst1ll3r --https
```

### Stopping the Server

While the server is running, press 'Q' and Enter to stop it gracefully.

## Client-Side File Upload

### PowerShell (Windows)

Use the following PowerShell command to upload a file:

For HTTP:
```powershell
$wc = New-Object System.Net.WebClient; $wc.Headers.Add("Authorization", "Basic " + [Convert]::ToBase64String([Text.Encoding]::ASCII.GetBytes("username:password"))); try { $response = $wc.UploadData("http://serverip:port", [System.IO.File]::ReadAllBytes("path\to\file")); Write-Host "Server response: $([System.Text.Encoding]::UTF8.GetString($response))"; Write-Host "File sent successfully!" } catch { Write-Host "An error occurred: $_" }
```

For HTTPS (ignoring SSL certificate errors):
```powershell
[System.Net.ServicePointManager]::ServerCertificateValidationCallback = {$true}; $wc = New-Object System.Net.WebClient; $wc.Headers.Add("Authorization", "Basic " + [Convert]::ToBase64String([Text.Encoding]::ASCII.GetBytes("username:password"))); try { $response = $wc.UploadData("https://serverip:port", [System.IO.File]::ReadAllBytes("path\to\file")); Write-Host "Server response: $([System.Text.Encoding]::UTF8.GetString($response))"; Write-Host "File sent successfully!" } catch { Write-Host "An error occurred: $_" }
```

### Linux

Use the following curl commands to upload a file:

For HTTP:
```bash
curl -X POST -u username:password -F "file=@/path/to/your/file" http://serverip:port
```

For HTTPS (ignoring SSL certificate errors):
```bash
curl -X POST -u username:password -F "file=@/path/to/your/file" -k https://serverip:port
```

Replace `username`, `password`, `serverip`, `port`, and `path\to\file` (or `/path/to/your/file` for Linux) with your specific values.

## Security Considerations

- Always use HTTPS in production environments.
- The self-signed certificate generated for HTTPS is not suitable for production use. Use a proper SSL certificate from a trusted Certificate Authority for production deployments.
- Regularly update the authentication credentials.
- Be cautious when using commands that ignore SSL certificate errors, as they bypass security checks.

## License

[MIT License](LICENSE)

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.
