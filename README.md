# Configuration-HTTPS-CertBot

Upon completion of certbot installation for the desired webserver it will present a message showing the path where the * .pem files are located. Enter the folder using the command "cd 'path...'" and execute the command below.<br/>
  
openssl pkcs12 -export -out bundle.pfx -inkey privkey.pem -in cert.pem -certfile chain.pem -password pass:xxx

The path where the .pfx file was generated must be accessible by your application.
Example:

    public static IWebHost BuildWebHost(string[] args) =>
			WebHost.CreateDefaultBuilder(args)
				.UseStartup<Startup>()
			.UseKestrel(options =>
			{
				//options.Listen(IPAddress.Any, 3000);

				options.Listen(IPAddress.Any, 3000, listenOptions =>
				{
					listenOptions.UseHttps(GetMyX509Certificate(@"/home/ubuntu/config/https.pfx", "xxx"));
				});

			})
				.Build();

		private static X509Certificate2 GetMyX509Certificate(string path, string password)
		{
			try
			{
				//X509Store store = new X509Store("My", StoreLocation.CurrentUser);
				X509Certificate2 cert;
				cert = new X509Certificate2(File.ReadAllBytes(path), password, X509KeyStorageFlags.MachineKeySet);
				bool result = cert.Verify();
				var r2 = result;
				return cert;
			}
			catch (Exception ex)
			{
				Console.Out.WriteLine("ErrorGettingCertificate in base:" + ex.Message);
				return null;
			}
		}

chmod 777 -R <<Directory or File>>
  
# Documantation pattern of CertBot Apache
  https://certbot.eff.org/lets-encrypt/ubuntubionic-apache
  
# Documantation pattern of CertBot NGinx
  https://certbot.eff.org/lets-encrypt/ubuntubionic-nginx
