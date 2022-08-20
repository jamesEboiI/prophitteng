- 👋 Hi, I’m @prophitteng
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
prophitteng/prophitteng is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
https://github.com/prophitteng/Hello-world.wiki.gitpublic class MainActivity extends Activity implements CreateNdefMessageCallback {
    Override
    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        NfcAdapter nfcAdapter = NfcAdapter.getDefaultAdapter(this);
        nfcAdapter.setNdefPushMessageCallback(this, this);
    }

    verride
    public NdefMessage createNdefMessage(NfcEvent event) {
        try {
            Properties p = new Properties();

            p.setProperty(
                    DevicePolicyManager.EXTRA_PROVISIONING_DEVICE_ADMIN_PACKAGE_NAME,
                    "apk package name");
            p.setProperty(
                    DevicePolicyManager.EXTRA_PROVISIONING_DEVICE_ADMIN_PACKAGE_DOWNLOAD_LOCATION,
                    "app download url");
            p.setProperty(
                    DevicePolicyManager.EXTRA_PROVISIONING_DEVICE_ADMIN_PACKAGE_CHECKSUM,
                    "apk checksum");
            ByteArrayOutputStream bos = new ByteArrayOutputStream();
            OutputStream out = new ObjectOutputStream(bos);
            p.store(out, "");
            final byte[] bytes = bos.toByteArray();

            NdefMessage msg = new NdefMessage(NdefRecord.createMime(
                    DevicePolicyManager.MIME_TYPE_PROVISIONING_NFC, bytes));
            return msg;
        } catch (Exception e) {
            throw new RuntimeException(e);
        }
    }
}
