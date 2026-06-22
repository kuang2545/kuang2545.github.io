
// ============================================================
// บันทึก OT — Flutter v6 "ThaID Style"  (+ หน้าเข้าสู่ระบบ)
// ธีมน้ำเงินกรมท่าแบบแอป ThaID: gradient header โค้ง,
// การ์ดขาวลอย, ไอคอนวงกลมฟ้าอ่อน, ปุ่มน้ำเงินไล่เฉด, accent ทอง
// Responsive: มือถือ 1 คอลัมน์ / จอกว้าง ≥900px 2 คอลัมน์
// วางทับ lib/OT.dart — dependencies: image_picker, geolocator
// ============================================================
import 'dart:convert';
import 'dart:typed_data';
import 'package:flutter/foundation.dart' show kIsWeb;
import 'package:flutter/services.dart'
    show rootBundle, TextInputFormatter, TextEditingValue;
import 'package:flutter/cupertino.dart';
import 'package:flutter/material.dart' show Icons;
import 'package:image_picker/image_picker.dart';
import 'package:geolocator/geolocator.dart';
import 'package:http/http.dart' as http;

const bool demoMode = false;

const String _demoPhoto =
    'data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAQAAAC1HAwCAAAAC0lEQVR42mNkYPhfDwAChwGA60e6kgAAAABJRU5ErkJggg==';
const String allowanceCompany = '3E Innovation';
const List<String> companies = [
  '3E Empire',
  '3E Trading',
  '3E Innovation',
  'AE&T',
  'Eita & Paul',
  'Hikari Denki',
  'Chavest',
];

// ---------- โทนสี ----------
const tDark = Color(0xFF2D4F7C);
const tOrange = Color(0xFF3E6CA0);
const tOrangeLight = Color(0xFF7BA3C9);
const tOrangeSoft = Color(0xFFF6F0E1);
const tGold = Color(0xFFEE8B33);
const tBg = Color(0xFFFEFEFC);
const tField = Color(0xFFFFFFFF);
const tText = Color(0xFF1F2D3D);
const tText2 = Color(0xFF8E99A8);
const tSage = Color(0xFF3E6CA0);
const tSageSoft = Color(0xFFF6F0E1);
const tBlueG = Color(0xFF3E6CA0);
const tRed = Color(0xFFD9534F);
const tGreen = Color(0xFF3E6CA0);
const tCreamLine = Color(0xFFEBE2D0);

const double kWide = 900;

const _headGrad = LinearGradient(
  begin: Alignment.topLeft,
  end: Alignment.bottomRight,
  colors: [tDark, tOrange, tOrangeLight],
);
const _btnGrad = LinearGradient(
  begin: Alignment.centerLeft,
  end: Alignment.centerRight,
  colors: [tDark, tOrange],
);
const _btnGradSage = LinearGradient(
  begin: Alignment.centerLeft,
  end: Alignment.centerRight,
  colors: [Color(0xFFD9731F), tGold],
);

const Curve kSmooth = Cubic(0.4, 0.0, 0.2, 1.0);

// แปลงตัวอักษรที่พิมพ์ให้เป็นตัวใหญ่อัตโนมัติ (รหัสพนักงาน)
class _UpperCaseFormatter extends TextInputFormatter {
  @override
  TextEditingValue formatEditUpdate(
      TextEditingValue oldValue, TextEditingValue newValue) {
    return newValue.copyWith(text: newValue.text.toUpperCase());
  }
}

void main() => runApp(const OtApp());

// ── API บันทึก OT (Apps Script — OT_Records) ──
// 👉 วาง URL /exec ของสคริปต์ OT_Records ที่ deploy แล้วตรงนี้
const String OT_API = 'https://script.google.com/macros/s/AKfycby_qTVYsGJx8zlNgK_u1L9AnGzDAlrbUUKPtUY846HgPZS2dCgHZKmqJcTKmFNvuhe5GA/exec';

// POST แล้วตาม redirect ของ Apps Script เอง (มือถือบางเครื่องไม่ตามให้)
Future<String> _apiPostFollow(String url, Map<String, dynamic> body) async {
  var current = url;
  http.Response res = await http
      .post(Uri.parse(current),
          headers: {'Content-Type': 'text/plain;charset=utf-8'},
          body: jsonEncode(body))
      .timeout(const Duration(seconds: 60));
  var hop = 0;
  while (!kIsWeb &&
      (res.statusCode == 301 ||
          res.statusCode == 302 ||
          res.statusCode == 303 ||
          res.statusCode == 307) &&
      res.headers['location'] != null &&
      hop < 5) {
    current = res.headers['location']!;
    res = await http.get(Uri.parse(current));
    hop++;
  }
  return res.body;
}

Future<Map<String, dynamic>> apiCall(
    String action, Map<String, dynamic> payload) async {
  if (OT_API == 'PASTE_OT_RECORDS_URL_HERE') {
    return {'success': false, 'message': 'ยังไม่ได้ตั้งค่า OT_API'};
  }
  try {
    final body = await _apiPostFollow(OT_API, {'action': action, ...payload});
    final j = jsonDecode(body);
    return Map<String, dynamic>.from(j);
  } catch (e) {
    return {'success': false, 'message': 'เชื่อมต่อไม่ได้: $e'};
  }
}

class OtApp extends StatelessWidget {
  const OtApp({super.key});
  @override
  Widget build(BuildContext context) {
    return CupertinoApp(
      title: 'บันทึก OT',
      debugShowCheckedModeBanner: false,
      theme: const CupertinoThemeData(
        brightness: Brightness.light,
        primaryColor: tOrange,
        scaffoldBackgroundColor: tBg,
        textTheme: CupertinoTextThemeData(
          textStyle: TextStyle(fontSize: 16, color: tText),
          actionTextStyle: TextStyle(fontSize: 16, color: tOrange),
          navTitleTextStyle: TextStyle(
              fontSize: 17, fontWeight: FontWeight.w600, color: tText),
          pickerTextStyle: TextStyle(fontSize: 21, color: tText),
          dateTimePickerTextStyle: TextStyle(fontSize: 21, color: tText),
        ),
      ),
      builder: (context, child) {
        if (!kIsWeb) return child!;
        // บนเว็บ: ถ้าจอแคบ (มือถือ/PWA) ให้เต็มจอเหมือนแอปจริง
        // ถ้าจอกว้าง (คอม) ค่อยโชว์กรอบมือถือลอยกลางจอไว้ดูเฉย ๆ
        final w = MediaQuery.of(context).size.width;
        if (w < 500) return child!;
        return ColoredBox(
          color: const Color(0xFFE7EAF0),
          child: Center(
            child: Container(
              width: 430,
              constraints: const BoxConstraints(maxHeight: 920),
              margin: const EdgeInsets.symmetric(vertical: 16),
              clipBehavior: Clip.antiAlias,
              decoration: BoxDecoration(
                color: tBg,
                borderRadius: BorderRadius.circular(36),
                boxShadow: const [
                  BoxShadow(
                      color: Color(0x33000000),
                      blurRadius: 40,
                      offset: Offset(0, 18)),
                ],
              ),
              child: child,
            ),
          ),
        );
      },
      home: const LoginPage(),
    );
  }
}

// ============================================================
// หน้าเข้าสู่ระบบ
// ============================================================

// ── API พนักงาน (Apps Script) ──
const String USER_API =
    'https://script.google.com/macros/s/AKfycbxsiLedShdopEiWpgx7nKqfM5PK4KS2NM3JlekAKFIybs2uG3Ktv0xAu1yeRYTYeDKmyQ/exec';

// เก็บข้อมูลพนักงานที่ล็อกอินไว้ใช้ทั้งแอป (ชื่อ/แผนก/ตำแหน่ง ฯลฯ)
Map<String, dynamic>? currentUser;

// ตรวจรหัสกับ API จริง → คืน {ok, message}
Future<Map<String, dynamic>> _checkLogin(String empId, String pass) async {
  try {
    final payload = jsonEncode({
      'action': 'login',
      'employeeId': empId.trim(),
      'password': pass,
    });
    // POST แล้วตาม redirect ของ Apps Script เอง (มือถือบางเครื่องไม่ตามให้)
    var url = USER_API;
    http.Response res = await http
        .post(Uri.parse(url),
            headers: {'Content-Type': 'text/plain;charset=utf-8'},
            body: payload)
        .timeout(const Duration(seconds: 30));
    // บนเว็บ เบราว์เซอร์ตาม redirect ให้เอง — ห้ามตามเอง(CORS อ่าน location ไม่ได้)
    var hop = 0;
    while (!kIsWeb &&
        (res.statusCode == 301 ||
            res.statusCode == 302 ||
            res.statusCode == 303 ||
            res.statusCode == 307) &&
        res.headers['location'] != null &&
        hop < 5) {
      url = res.headers['location']!;
      res = await http.get(Uri.parse(url));
      hop++;
    }
    final j = jsonDecode(res.body);
    if (j['success'] == true) {
      currentUser = (j['user'] is Map)
          ? Map<String, dynamic>.from(j['user'])
          : null;
      return {'ok': true};
    }
    return {'ok': false, 'message': j['message'] ?? 'เข้าสู่ระบบไม่สำเร็จ'};
  } catch (e) {
    return {'ok': false, 'message': 'เชื่อมต่อไม่ได้: $e'};
  }
}

class LoginPage extends StatefulWidget {
  const LoginPage({super.key});
  @override
  State<LoginPage> createState() => _LoginPageState();
}

class _LoginPageState extends State<LoginPage> {
  final userCtrl = TextEditingController();
  bool busy = false;
  String error = '';
  Uint8List? _logoBytes; // รูปโลโก้ (ถ้าโหลดได้)
  int step = 0; // 0 = ใส่รหัสพนักงาน, 1 = ใส่ PIN
  String pin = ''; // รหัสผ่านที่กดอยู่
  String empId = ''; // รหัสพนักงานที่ยืนยันแล้ว
  String empName = ''; // ชื่อพนักงาน (โชว์ตอนใส่ PIN)

  @override
  void initState() {
    super.initState();
    _loadLogo();
  }

  Future<void> _loadLogo() async {
    const candidates = [
      'assets/icon/logoOT.png',
      'assets/icon/OT.png',
      'assets/logoOT.png',
    ];
    for (final path in candidates) {
      try {
        final data = await rootBundle.load(path);
        if (mounted) setState(() => _logoBytes = data.buffer.asUint8List());
        return;
      } catch (_) {}
    }
  }

  // ดึงรายชื่อพนักงาน (GET) เพื่อตรวจว่ามีรหัสนี้ไหม + ได้ชื่อมาโชว์
  Future<Map<String, dynamic>?> _findUser(String id) async {
    final body = await _httpGetFollow(USER_API);
    final j = jsonDecode(body);
    if (j['status'] != 'ok' || j['data'] is! List) return null;
    final target = id.trim().toUpperCase();
    for (final u in (j['data'] as List)) {
      if (u is Map &&
          u['employee_id'].toString().trim().toUpperCase() == target) {
        return Map<String, dynamic>.from(u);
      }
    }
    return null;
  }

  // GET ที่ตาม redirect ของ Apps Script เอง (มือถือบางเครื่องไม่ตามให้)
  // บนเว็บ: ใช้ http.get ปกติ (เบราว์เซอร์ตาม redirect ให้เอง — อ่าน location header ไม่ได้เพราะ CORS)
  Future<String> _httpGetFollow(String url) async {
    if (kIsWeb) {
      final res = await http.get(Uri.parse(url));
      return res.body;
    }
    var current = url;
    for (var i = 0; i < 5; i++) {
      final req = http.Request('GET', Uri.parse(current))
        ..followRedirects = false;
      final streamed = await req.send();
      final res = await http.Response.fromStream(streamed);
      if (res.statusCode == 301 ||
          res.statusCode == 302 ||
          res.statusCode == 303 ||
          res.statusCode == 307) {
        final loc = res.headers['location'];
        if (loc == null) break;
        current = loc;
        continue;
      }
      return res.body;
    }
    throw Exception('redirect เยอะเกินไป');
  }

  // สเต็ป 1 → ยืนยันรหัสพนักงาน ถ้ามี เด้งแป้น PIN
  Future<void> _next() async {
    FocusScope.of(context).unfocus(); // ปิดแป้นพิมพ์ กันข้อมูลเบียดล้น
    final id = userCtrl.text.trim().toUpperCase();
    setState(() => error = '');
    if (id.isEmpty) {
      setState(() => error = 'กรุณากรอกรหัสพนักงาน');
      return;
    }
    setState(() => busy = true);
    try {
      final u = await _findUser(id);
      setState(() => busy = false);
      if (u != null) {
        setState(() {
          empId = id;
          empName = (u['full_name'] ?? '').toString();
          pin = '';
          step = 1;
        });
      } else {
        setState(() => error = 'ไม่พบรหัสพนักงานนี้');
      }
    } catch (e) {
      setState(() {
        busy = false;
        error = 'เชื่อมต่อไม่ได้: $e';
      });
    }
  }

  void _onKey(String d) {
    if (busy || pin.length >= 4) return;
    setState(() {
      pin += d;
      error = '';
    });
    if (pin.length == 4) _verifyPin();
  }

  void _del() {
    if (pin.isEmpty) return;
    setState(() => pin = pin.substring(0, pin.length - 1));
  }

  void _backToId() {
    setState(() {
      step = 0;
      pin = '';
      error = '';
    });
  }

  // สเต็ป 2 → ตรวจ PIN กับ API
  Future<void> _verifyPin() async {
    setState(() => busy = true);
    try {
      final res = await _checkLogin(empId, pin);
      setState(() => busy = false);
      if (res['ok'] == true) {
        if (!mounted) return;
        _goHome();
      } else {
        setState(() {
          pin = '';
          error = res['message'] ?? 'รหัสผ่านไม่ถูกต้อง';
        });
      }
    } catch (e) {
      setState(() {
        busy = false;
        pin = '';
        error = 'เข้าสู่ระบบไม่สำเร็จ: $e';
      });
    }
  }

  void _goHome() {
    Navigator.pushReplacement(
      context,
      PageRouteBuilder(
        transitionDuration: const Duration(milliseconds: 300),
        pageBuilder: (_, __, ___) => const HomePage(),
        transitionsBuilder: (_, animation, __, child) {
          final curved = CurvedAnimation(parent: animation, curve: kSmooth);
          return FadeTransition(
            opacity: curved,
            child: SlideTransition(
              position: Tween<Offset>(
                begin: const Offset(0, 0.12),
                end: Offset.zero,
              ).animate(curved),
              child: child,
            ),
          );
        },
      ),
    );
  }

  // ── เนื้อหาในการ์ดตามสเต็ป ──
  List<Widget> _stepContent() => step == 0 ? _idStep() : _pinStep();

  List<Widget> _idStep() => [
        _loginField(
          label: 'รหัสพนักงาน',
          ctrl: userCtrl,
          placeholder: 'กรอกรหัสพนักงาน',
          icon: Icons.badge_rounded,
        ),
        if (error.isNotEmpty) _errorRow(),
        const SizedBox(height: 18),
        _bigButton(busy ? null : _next, busy, 'ถัดไป'),
        const SizedBox(height: 4),
      ];

  List<Widget> _pinStep() => [
        Center(
          child: Text(empName.isEmpty ? 'ใส่รหัสผ่าน' : empName,
              style: const TextStyle(
                  fontSize: 17, fontWeight: FontWeight.w700, color: tText)),
        ),
        const SizedBox(height: 4),
        const Center(
          child: Text('ใส่รหัสผ่าน 4 หลัก',
              style: TextStyle(fontSize: 12.5, color: tText2)),
        ),
        const SizedBox(height: 20),
        _pinDots(),
        SizedBox(
          height: 22,
          child: error.isNotEmpty
              ? Center(
                  child: Text(error,
                      style: const TextStyle(color: tRed, fontSize: 13)))
              : (busy
                  ? const Center(child: CupertinoActivityIndicator(radius: 8))
                  : null),
        ),
        const SizedBox(height: 8),
        _keypad(),
        const SizedBox(height: 6),
        Center(
          child: CupertinoButton(
            padding: const EdgeInsets.symmetric(vertical: 8),
            onPressed: _backToId,
            child: const Text('เปลี่ยนรหัสพนักงาน',
                style: TextStyle(fontSize: 13, color: tOrange)),
          ),
        ),
      ];

  Widget _errorRow() => Padding(
        padding: const EdgeInsets.only(top: 12),
        child: Row(
          children: [
            const Icon(Icons.error_rounded, size: 16, color: tRed),
            const SizedBox(width: 6),
            Expanded(
              child: Text(error,
                  style: const TextStyle(color: tRed, fontSize: 13)),
            ),
          ],
        ),
      );

  Widget _bigButton(VoidCallback? onTap, bool loading, String label) =>
      GestureDetector(
        onTap: onTap,
        child: Container(
          padding: const EdgeInsets.symmetric(vertical: 15),
          alignment: Alignment.center,
          decoration: BoxDecoration(
            gradient: _btnGrad,
            borderRadius: BorderRadius.circular(14),
            boxShadow: [
              BoxShadow(
                  color: tOrange.withOpacity(0.35),
                  blurRadius: 16,
                  offset: const Offset(0, 6)),
            ],
          ),
          child: loading
              ? const CupertinoActivityIndicator(color: CupertinoColors.white)
              : Text(label,
                  style: const TextStyle(
                      fontSize: 17,
                      fontWeight: FontWeight.w700,
                      color: CupertinoColors.white)),
        ),
      );

  Widget _pinDots() => Row(
        mainAxisAlignment: MainAxisAlignment.center,
        children: List.generate(4, (i) {
          final filled = i < pin.length;
          return Container(
            margin: const EdgeInsets.symmetric(horizontal: 10),
            width: 16,
            height: 16,
            decoration: BoxDecoration(
              shape: BoxShape.circle,
              color: filled ? tOrange : const Color(0x00000000),
              border: Border.all(
                  color: filled ? tOrange : const Color(0xFFC7D0DD),
                  width: 1.6),
            ),
          );
        }),
      );

  Widget _keypad() {
    const keys = ['1', '2', '3', '4', '5', '6', '7', '8', '9', '', '0', 'del'];
    return GridView.count(
      crossAxisCount: 3,
      shrinkWrap: true,
      physics: const NeverScrollableScrollPhysics(),
      mainAxisSpacing: 10,
      crossAxisSpacing: 10,
      childAspectRatio: 1.6,
      children: keys.map((k) {
        if (k == '') return const SizedBox();
        if (k == 'del') {
          return _keyBtn(
            onTap: _del,
            child: const Icon(Icons.backspace_rounded,
                size: 22, color: tText2),
          );
        }
        return _keyBtn(
          onTap: () => _onKey(k),
          child: Text(k,
              style: const TextStyle(
                  fontSize: 24, fontWeight: FontWeight.w600, color: tText)),
        );
      }).toList(),
    );
  }

  Widget _keyBtn({required Widget child, required VoidCallback onTap}) =>
      GestureDetector(
        onTap: busy ? null : onTap,
        child: Container(
          alignment: Alignment.center,
          decoration: BoxDecoration(
            color: const Color(0xFFF4F6FA),
            borderRadius: BorderRadius.circular(14),
          ),
          child: child,
        ),
      );

  @override
  Widget build(BuildContext context) {
    return CupertinoPageScaffold(
      child: LayoutBuilder(builder: (context, c) {
        final h = c.maxHeight;
        return SingleChildScrollView(
          child: ConstrainedBox(
            constraints: BoxConstraints(minHeight: h),
            child: Stack(
              children: [
                // ── พื้นหลังน้ำเงินยาวลงไป (อยู่หลังการ์ด) ──
                Container(
                  width: double.infinity,
                  height: h * 0.85,
                  decoration: const BoxDecoration(
                    gradient: _headGrad,
                    borderRadius:
                        BorderRadius.vertical(bottom: Radius.circular(36)),
                  ),
                ),
                // ── เนื้อหา: หัว + การ์ด ──
                Column(
                  children: [
                    SizedBox(
                      height: h * (step == 0 ? 0.44 : 0.35),
                      child: SafeArea(
                        bottom: false,
                        child: FittedBox(
                          fit: BoxFit.scaleDown,
                          child: Column(
                          mainAxisAlignment: MainAxisAlignment.center,
                          children: [
                        Container(
                          width: 104,
                          height: 104,
                          decoration: BoxDecoration(
                            color: _logoBytes != null
                                ? CupertinoColors.white
                                : const Color(0x26FFFFFF),
                            shape: BoxShape.circle,
                            border: Border.all(
                                color: const Color(0x4DFFFFFF), width: 1.5),
                            boxShadow: _logoBytes != null
                                ? const [
                                    BoxShadow(
                                        color: Color(0x22000000),
                                        blurRadius: 16,
                                        offset: Offset(0, 6)),
                                  ]
                                : null,
                          ),
                          clipBehavior: Clip.antiAlias,
                          child: _logoBytes != null
                              ? Image.memory(_logoBytes!, fit: BoxFit.cover)
                              : const Icon(Icons.access_time_filled_rounded,
                                  color: CupertinoColors.white, size: 46),
                        ),
                        const SizedBox(height: 18),
                        const Text('บันทึก OT',
                            style: TextStyle(
                                fontSize: 26,
                                fontWeight: FontWeight.w700,
                                color: CupertinoColors.white)),
                        const SizedBox(height: 8),
                        Container(
                            height: 3,
                            width: 48,
                            decoration: BoxDecoration(
                                color: tGold,
                                borderRadius: BorderRadius.circular(2))),
                        const SizedBox(height: 12),
                        const Text('เข้าสู่ระบบเพื่อเริ่มใช้งาน',
                            style: TextStyle(
                                fontSize: 13, color: Color(0xCCFFFFFF))),
                      ],
                    ),
                    ),
                  ),
                ),
                    // ── การ์ด login ลอยทับน้ำเงิน ──
                    Center(
                    child: ConstrainedBox(
                      constraints: const BoxConstraints(maxWidth: 420),
                      child: Padding(
                        padding: const EdgeInsets.fromLTRB(24, 0, 24, 8),
                        child: Container(
                          padding: const EdgeInsets.all(22),
                          decoration: BoxDecoration(
                            color: CupertinoColors.white,
                            borderRadius: BorderRadius.circular(18),
                            border: Border.all(color: tCreamLine),
                            boxShadow: const [
                              BoxShadow(
                                  color: Color(0x1F0F172A),
                                  blurRadius: 28,
                                  offset: Offset(0, 10)),
                            ],
                          ),
                          child: Column(
                            crossAxisAlignment: CrossAxisAlignment.stretch,
                            children: _stepContent(),
                          ),
                        ),
                      ),
                    ),
                  ),
                  ],
                ),
              ],
            ),
          ),
        );
      }),
    );
  }

  Widget _loginField({
    required String label,
    required TextEditingController ctrl,
    required String placeholder,
    required IconData icon,
    bool obscure = false,
    Widget? trailing,
  }) {
    return Container(
      padding: const EdgeInsets.symmetric(horizontal: 14, vertical: 6),
      decoration: BoxDecoration(
        color: tField,
        borderRadius: BorderRadius.circular(12),
        border: Border.all(color: const Color(0xFFE9EEF5)),
      ),
      child: Row(
        children: [
          Icon(icon, size: 20, color: tText2),
          const SizedBox(width: 10),
          Expanded(
            child: Column(
              crossAxisAlignment: CrossAxisAlignment.start,
              children: [
                Text(label,
                    style: const TextStyle(fontSize: 11.5, color: tText2)),
                CupertinoTextField(
                  controller: ctrl,
                  placeholder: placeholder,
                  obscureText: obscure,
                  textCapitalization: TextCapitalization.characters,
                  inputFormatters: [_UpperCaseFormatter()],
                  padding: const EdgeInsets.only(top: 2, bottom: 4),
                  style: const TextStyle(
                      fontSize: 16,
                      fontWeight: FontWeight.w600,
                      color: tText),
                  placeholderStyle: const TextStyle(
                      fontSize: 15, color: Color(0xFFAEB6C6)),
                  decoration: const BoxDecoration(color: Color(0x00000000)),
                  onSubmitted: (_) => _next(),
                ),
              ],
            ),
          ),
          if (trailing != null) trailing,
        ],
      ),
    );
  }
}

// ============================================================
// หน้าแรก
// ============================================================
class HomePage extends StatelessWidget {
  const HomePage({super.key});

  void _open(BuildContext context, bool isClockOut) => Navigator.push(
        context,
        PageRouteBuilder(
          transitionDuration: const Duration(milliseconds: 300),
          reverseTransitionDuration: const Duration(milliseconds: 300),
          pageBuilder: (_, __, ___) => FormPage(isClockOut: isClockOut),
          transitionsBuilder: (_, animation, __, child) {
            final curved = CurvedAnimation(
              parent: animation,
              curve: kSmooth,
              reverseCurve: kSmooth,
            );
            return FadeTransition(
              opacity: curved,
              child: SlideTransition(
                position: Tween<Offset>(
                  begin: const Offset(0, 0.12),
                  end: Offset.zero,
                ).animate(curved),
                child: child,
              ),
            );
          },
        ),
      );

  void _logout(BuildContext context) {
    showCupertinoDialog(
      context: context,
      builder: (_) => CupertinoAlertDialog(
        title: const Text('ออกจากระบบ'),
        content: const Padding(
          padding: EdgeInsets.only(top: 6),
          child: Text('ต้องการออกจากระบบใช่ไหม?'),
        ),
        actions: [
          CupertinoDialogAction(
            onPressed: () => Navigator.pop(context),
            child: const Text('ยกเลิก'),
          ),
          CupertinoDialogAction(
            isDestructiveAction: true,
            onPressed: () {
              Navigator.pop(context);
              Navigator.pushReplacement(
                context,
                CupertinoPageRoute(builder: (_) => const LoginPage()),
              );
            },
            child: const Text('ออกจากระบบ'),
          ),
        ],
      ),
    );
  }

  @override
  Widget build(BuildContext context) {
    final secondary =
        ModalRoute.of(context)?.secondaryAnimation ?? kAlwaysDismissedAnimation;
    return CupertinoPageScaffold(
      child: AnimatedBuilder(
        animation: secondary,
        builder: (context, child) {
          final s = kSmooth.transform(secondary.value.clamp(0.0, 1.0));
          return FractionalTranslation(
            translation: Offset(0.22 * s, 0),
            child: child,
          );
        },
        child: LayoutBuilder(builder: (context, c) {
          final wide = c.maxWidth >= kWide;
          return wide ? _buildWide(context) : _buildNarrow(context);
        }),
      ),
    );
  }

  Widget _buildNarrow(BuildContext context) {
    return Column(
      children: [
        Expanded(
          child: SingleChildScrollView(
            child: Column(
        children: [
          Stack(
            children: [
              const Positioned(
                top: 0,
                left: 0,
                right: 0,
                child: SizedBox(
                  height: 380,
                  child: DecoratedBox(
                    decoration: BoxDecoration(
                      gradient: _headGrad,
                      borderRadius:
                          BorderRadius.vertical(bottom: Radius.circular(32)),
                    ),
                  ),
                ),
              ),
              Column(
                children: [
                  SafeArea(
                    bottom: false,
                    child: Padding(
                      padding: const EdgeInsets.fromLTRB(20, 14, 8, 8),
                      child: Row(
                        children: [
                          const Expanded(
                            child: Column(
                              mainAxisSize: MainAxisSize.min,
                              crossAxisAlignment: CrossAxisAlignment.start,
                              children: [
                                Text('บันทึก OT',
                                    style: TextStyle(
                                        fontSize: 22,
                                        fontWeight: FontWeight.w700,
                                        color: CupertinoColors.white)),
                                Text('ระบบบันทึกเวลาทำงานล่วงเวลา',
                                    style: TextStyle(
                                        fontSize: 12.5,
                                        color: Color(0xCCFFFFFF))),
                              ],
                            ),
                          ),
                          _logoutBtn(context),
                        ],
                      ),
                    ),
                  ),
                  const SizedBox(height: 18),
                  const Padding(
                    padding: EdgeInsets.symmetric(horizontal: 20),
                    child: _ClockCard(),
                  ),
                  const SizedBox(height: 18),
                  Padding(
                    padding: const EdgeInsets.symmetric(horizontal: 20),
                    child: Column(
                      crossAxisAlignment: CrossAxisAlignment.start,
                      children: [
                        _menuCard(context,
                            icon: Icons.play_circle_rounded,
                            title: 'เริ่มงาน',
                            subtitle: 'บันทึกเวลาเข้าเริ่ม OT',
                            isClockOut: false,
                            iconColor: tSage,
                            iconBg: tSageSoft),
                        const SizedBox(height: 12),
                        _menuCard(context,
                            icon: Icons.flag_circle_rounded,
                            title: 'เลิกงาน',
                            subtitle: 'เลือกชื่อ + บันทึกเวลาเลิก',
                            isClockOut: true),
                        const SizedBox(height: 18),
                        _stepsCard(),
                        const SizedBox(height: 12),
                        _noticeCard(),
                        const SizedBox(height: 24),
                      ],
                    ),
                  ),
                ],
              ),
            ],
          ),
        ],
            ),
          ),
        ),
        const SafeArea(
          top: false,
          child: Padding(
            padding: EdgeInsets.fromLTRB(20, 8, 20, 14),
            child: Text(
              'กด "เริ่มงาน" ก่อนเริ่มทำ OT แล้วกลับมากด "เลิกงาน" เมื่อทำเสร็จ',
              textAlign: TextAlign.center,
              style: TextStyle(fontSize: 12.5, color: tText2),
            ),
          ),
        ),
      ],
    );
  }

  Widget _buildWide(BuildContext context) {
    return SafeArea(
      child: Column(
        children: [
          Align(
            alignment: Alignment.centerRight,
            child: Padding(
              padding: const EdgeInsets.fromLTRB(0, 8, 20, 0),
              child: _logoutBtn(context, dark: true),
            ),
          ),
          Expanded(
            child: Center(
              child: ConstrainedBox(
          constraints: const BoxConstraints(maxWidth: 1000),
          child: Padding(
            padding: const EdgeInsets.all(32),
            child: Row(
              children: [
                Expanded(
                  flex: 11,
                  child: Container(
                    padding: const EdgeInsets.all(36),
                    decoration: BoxDecoration(
                      gradient: _headGrad,
                      borderRadius: BorderRadius.circular(28),
                      boxShadow: const [
                        BoxShadow(
                            color: Color(0x333E6CA0),
                            blurRadius: 32,
                            offset: Offset(0, 14)),
                      ],
                    ),
                    child: Column(
                      crossAxisAlignment: CrossAxisAlignment.center,
                      mainAxisAlignment: MainAxisAlignment.center,
                      children: [
                        const Text('บันทึก OT',
                            style: TextStyle(
                                fontSize: 24,
                                fontWeight: FontWeight.w700,
                                color: CupertinoColors.white)),
                        const SizedBox(height: 8),
                        Container(
                            height: 3,
                            width: 56,
                            decoration: BoxDecoration(
                                color: tGold,
                                borderRadius: BorderRadius.circular(2))),
                        const SizedBox(height: 28),
                        const _LiveTime(
                            align: CrossAxisAlignment.center,
                            timeStyle: TextStyle(
                                fontSize: 72,
                                fontWeight: FontWeight.w700,
                                color: CupertinoColors.white,
                                letterSpacing: -2,
                                fontFeatures: [FontFeature.tabularFigures()]),
                            dateStyle: TextStyle(
                                fontSize: 16, color: Color(0xCCFFFFFF))),
                      ],
                    ),
                  ),
                ),
                const SizedBox(width: 28),
                Expanded(
                  flex: 9,
                  child: Column(
                    mainAxisAlignment: MainAxisAlignment.center,
                    children: [
                      _menuCard(context,
                          icon: Icons.play_circle_rounded,
                          title: 'เริ่มงาน',
                          subtitle: 'บันทึกเวลาเข้าเริ่ม OT',
                          isClockOut: false,
                          iconColor: tSage,
                          iconBg: tSageSoft),
                      const SizedBox(height: 14),
                      _menuCard(context,
                          icon: Icons.flag_circle_rounded,
                          title: 'เลิกงาน',
                          subtitle: 'เลือกชื่อ + บันทึกเวลาเลิก',
                          isClockOut: true),
                      const SizedBox(height: 16),
                      _stepsCard(),
                      const SizedBox(height: 12),
                      _noticeCard(),
                    ],
                  ),
                ),
              ],
            ),
          ),
        ),
      ),
          ),
          const Padding(
            padding: EdgeInsets.only(bottom: 16, left: 20, right: 20),
            child: Text(
              'กด "เริ่มงาน" ก่อนเริ่มทำ OT แล้วกลับมากด "เลิกงาน" เมื่อทำเสร็จ',
              textAlign: TextAlign.center,
              style: TextStyle(fontSize: 12.5, color: tText2),
            ),
          ),
        ],
      ),
    );
  }

  Widget _logoutBtn(BuildContext context, {bool dark = false}) {
    return GestureDetector(
      onTap: () => _logout(context),
      child: Container(
        padding: const EdgeInsets.symmetric(horizontal: 12, vertical: 7),
        decoration: BoxDecoration(
          color: dark ? const Color(0x14000000) : const Color(0x2EFFFFFF),
          borderRadius: BorderRadius.circular(99),
          border: Border.all(
              color: dark ? const Color(0x22000000) : const Color(0x4DFFFFFF)),
        ),
        child: Row(
          mainAxisSize: MainAxisSize.min,
          children: [
            Icon(Icons.logout_rounded,
                size: 14, color: dark ? tText2 : CupertinoColors.white),
            const SizedBox(width: 5),
            Text('ออกจากระบบ',
                style: TextStyle(
                    fontSize: 12.5,
                    fontWeight: FontWeight.w600,
                    color: dark ? tText2 : CupertinoColors.white)),
          ],
        ),
      ),
    );
  }

  Widget _stepsCard() {
    Widget step(String n, String title, String desc) => Padding(
          padding: const EdgeInsets.only(bottom: 14),
          child: Row(
            crossAxisAlignment: CrossAxisAlignment.start,
            children: [
              Container(
                width: 28,
                height: 28,
                alignment: Alignment.center,
                decoration: const BoxDecoration(
                    color: tOrange, shape: BoxShape.circle),
                child: Text(n,
                    style: const TextStyle(
                        color: CupertinoColors.white,
                        fontSize: 13.5,
                        fontWeight: FontWeight.w700)),
              ),
              const SizedBox(width: 12),
              Expanded(
                child: Column(
                  crossAxisAlignment: CrossAxisAlignment.start,
                  children: [
                    Text(title,
                        style: const TextStyle(
                            fontSize: 14.5,
                            fontWeight: FontWeight.w700,
                            color: tText)),
                    Text(desc,
                        style: const TextStyle(
                            fontSize: 12.5, color: tText2)),
                  ],
                ),
              ),
            ],
          ),
        );
    return Container(
      width: double.infinity,
      padding: const EdgeInsets.fromLTRB(18, 18, 18, 4),
      decoration: BoxDecoration(
        color: CupertinoColors.white,
        borderRadius: BorderRadius.circular(16),
        border: Border.all(color: const Color(0xFFF8F5EF)),
      ),
      child: Column(
        crossAxisAlignment: CrossAxisAlignment.start,
        children: [
          Row(
            children: [
              Container(
                  width: 3.5,
                  height: 16,
                  decoration: BoxDecoration(
                      color: tGold,
                      borderRadius: BorderRadius.circular(2))),
              const SizedBox(width: 8),
              const Text('ขั้นตอนการใช้งาน',
                  style: TextStyle(
                      fontSize: 15.5,
                      fontWeight: FontWeight.w700,
                      color: tDark)),
            ],
          ),
          const SizedBox(height: 14),
          step('1', 'กด "เริ่มงาน"', 'กรอกชื่อ เลือกบริษัท แล้วถ่ายรูปยืนยัน'),
          step('2', 'ทำงาน OT ตามปกติ', 'ระบบบันทึกเวลาเริ่มไว้ให้เรียบร้อย'),
          step('3', 'กลับมากด "เลิกงาน"',
              'เลือกชื่อตัวเอง ระบบคำนวณชั่วโมงให้อัตโนมัติ'),
        ],
      ),
    );
  }

  Widget _noticeCard() {
    return Container(
      width: double.infinity,
      padding: const EdgeInsets.all(14),
      decoration: BoxDecoration(
        color: tOrangeSoft,
        borderRadius: BorderRadius.circular(14),
      ),
      child: const Row(
        children: [
          Icon(Icons.verified_user_rounded, color: tGold, size: 26),
          SizedBox(width: 12),
          Expanded(
            child: Text(
                'ทุกการบันทึกจะแนบรูปถ่ายสดและพิกัด GPS เพื่อยืนยันตัวตนโดยอัตโนมัติ',
                style:
                    TextStyle(fontSize: 12.5, color: tText, height: 1.4)),
          ),
        ],
      ),
    );
  }

  Widget _menuCard(BuildContext context,
      {required IconData icon,
      required String title,
      required String subtitle,
      required bool isClockOut,
      Color iconColor = tGold,
      Color iconBg = tOrangeSoft}) {
    return GestureDetector(
      onTap: () => _open(context, isClockOut),
      child: Container(
        padding: const EdgeInsets.all(18),
        decoration: BoxDecoration(
          color: CupertinoColors.white,
          borderRadius: BorderRadius.circular(16),
          border: Border.all(color: tCreamLine),
          boxShadow: const [
            BoxShadow(
                color: Color(0x100F172A),
                blurRadius: 14,
                offset: Offset(0, 4)),
          ],
        ),
        child: Row(
          children: [
            Container(
              width: 52,
              height: 52,
              decoration: BoxDecoration(
                color: iconBg,
                shape: BoxShape.circle,
              ),
              child: Icon(icon, color: iconColor, size: 28),
            ),
            const SizedBox(width: 16),
            Expanded(
              child: Column(
                crossAxisAlignment: CrossAxisAlignment.start,
                children: [
                  Text(title,
                      style: const TextStyle(
                          fontSize: 17,
                          fontWeight: FontWeight.w700,
                          color: tText)),
                  Text(subtitle,
                      style:
                          const TextStyle(fontSize: 13, color: tText2)),
                ],
              ),
            ),
            const Icon(Icons.chevron_right_rounded,
                size: 18, color: Color(0xFFC9C2AF)),
          ],
        ),
      ),
    );
  }
}

// ---------- นาฬิกาสด ----------
class _LiveTime extends StatelessWidget {
  final TextStyle timeStyle;
  final TextStyle dateStyle;
  final CrossAxisAlignment align;
  const _LiveTime({
    required this.timeStyle,
    required this.dateStyle,
    this.align = CrossAxisAlignment.start,
  });

  static const _days = [
    'จันทร์', 'อังคาร', 'พุธ', 'พฤหัสบดี', 'ศุกร์', 'เสาร์', 'อาทิตย์'
  ];
  static const _months = [
    'ม.ค.', 'ก.พ.', 'มี.ค.', 'เม.ย.', 'พ.ค.', 'มิ.ย.',
    'ก.ค.', 'ส.ค.', 'ก.ย.', 'ต.ค.', 'พ.ย.', 'ธ.ค.'
  ];

  @override
  Widget build(BuildContext context) {
    final ta = align == CrossAxisAlignment.center
        ? TextAlign.center
        : TextAlign.start;
    return StreamBuilder(
      stream: Stream.periodic(const Duration(seconds: 1)),
      builder: (context, _) {
        final now = DateTime.now();
        final t =
            '${now.hour.toString().padLeft(2, '0')}:${now.minute.toString().padLeft(2, '0')}:${now.second.toString().padLeft(2, '0')}';
        final d =
            'วัน${_days[now.weekday - 1]}ที่ ${now.day} ${_months[now.month - 1]} ${now.year + 543}';
        return Column(
          crossAxisAlignment: align,
          children: [
            Text(t, textAlign: ta, style: timeStyle),
            const SizedBox(height: 2),
            Text(d, textAlign: ta, style: dateStyle),
          ],
        );
      },
    );
  }
}

class _ClockCard extends StatelessWidget {
  const _ClockCard();
  @override
  Widget build(BuildContext context) {
    return Container(
      padding: const EdgeInsets.symmetric(vertical: 20, horizontal: 24),
      decoration: BoxDecoration(
        color: CupertinoColors.white,
        borderRadius: BorderRadius.circular(18),
        border: Border.all(color: tCreamLine),
        boxShadow: const [
          BoxShadow(
              color: Color(0x140F172A), blurRadius: 24, offset: Offset(0, 8)),
        ],
      ),
      child: const Center(
        child: _LiveTime(
          align: CrossAxisAlignment.center,
          timeStyle: TextStyle(
              fontSize: 42,
              fontWeight: FontWeight.w700,
              color: tDark,
              letterSpacing: -1,
              fontFeatures: [FontFeature.tabularFigures()]),
          dateStyle: TextStyle(fontSize: 13.5, color: tText2),
        ),
      ),
    );
  }
}

// ============================================================
// หน้าฟอร์ม
// ============================================================
class FormPage extends StatefulWidget {
  final bool isClockOut;
  const FormPage({super.key, required this.isClockOut});
  @override
  State<FormPage> createState() => _FormPageState();
}

class _FormPageState extends State<FormPage> {
  DateTime otDate = DateTime.now();
  DateTime time = DateTime.now();
  final nameCtrl = TextEditingController();
  final supervisorCtrl = TextEditingController();
  final detailCtrl = TextEditingController();
  String company = '';
  String worktype = '';
  String department = ''; // แผนก (ดึงจากข้อมูลล็อกอิน)

  String? photoBase64;
  String photoSource = '';
  String photoTimestamp = '';

  Position? gps;
  String gpsStatus = 'กำลังหา GPS...';
  bool gpsOk = false;

  List<Map<String, dynamic>> activeList = [];
  int selectedIdx = -1;
  bool loadingActive = false;

  bool busy = false;
  String error = '';

  bool get isClockOut => widget.isClockOut;
  Map<String, dynamic>? get picked =>
      (selectedIdx >= 0 && selectedIdx < activeList.length)
          ? activeList[selectedIdx]
          : null;
  String get selectedCompany =>
      isClockOut ? (picked?['company'] ?? '') : company;
  bool get showWorktype => selectedCompany == allowanceCompany;
  Color get accent => isClockOut ? tGold : tOrange;
  LinearGradient get btnGrad => isClockOut ? _btnGradSage : _btnGrad;

  @override
  void initState() {
    super.initState();
    // เติมชื่อ-สกุล + แผนก(เอาจากตำแหน่ง คอลัมน์ D) จากข้อมูลที่ล็อกอิน
    if (!isClockOut && currentUser != null) {
      nameCtrl.text = (currentUser!['full_name'] ?? '').toString();
      department = (currentUser!['position'] ?? '').toString();
    }
    _startGps();
    if (isClockOut) _loadActive();
  }

  String _dateStr(DateTime d) =>
      '${d.year}-${d.month.toString().padLeft(2, '0')}-${d.day.toString().padLeft(2, '0')}';
  String _timeStr(DateTime t) =>
      '${t.hour.toString().padLeft(2, '0')}:${t.minute.toString().padLeft(2, '0')}';
  String _dateThai(DateTime d) => '${d.day}/${d.month}/${d.year + 543}';

  Future<void> _startGps() async {
    setState(() {
      gpsStatus = 'กำลังหา GPS...';
      gpsOk = false;
    });
    if (demoMode) {
      await Future.delayed(const Duration(milliseconds: 400));
      setState(() {
        gps = Position(
          latitude: 13.7563,
          longitude: 100.5018,
          timestamp: DateTime.now(),
          accuracy: 8,
          altitude: 0,
          altitudeAccuracy: 0,
          heading: 0,
          headingAccuracy: 0,
          speed: 0,
          speedAccuracy: 0,
        );
        gpsOk = true;
        gpsStatus = '±8 ม. (จำลอง)';
      });
      return;
    }
    try {
      if (!await Geolocator.isLocationServiceEnabled()) {
        setState(() => gpsStatus = 'เปิด GPS ในมือถือก่อน');
        return;
      }
      var perm = await Geolocator.checkPermission();
      if (perm == LocationPermission.denied) {
        perm = await Geolocator.requestPermission();
      }
      if (perm == LocationPermission.deniedForever) {
        setState(() => gpsStatus = 'ปิดสิทธิ์ถาวร — แตะเพื่อตั้งค่า');
        await Geolocator.openAppSettings();
        return;
      }
      if (perm == LocationPermission.denied) {
        setState(() => gpsStatus = 'ไม่ได้รับอนุญาต');
        return;
      }
      setState(() => gpsStatus = 'กำลังหา GPS...');
      Position? pos;
      for (final acc in [
        LocationAccuracy.high,
        LocationAccuracy.medium,
        LocationAccuracy.low,
      ]) {
        try {
          pos = await Geolocator.getCurrentPosition(
            locationSettings: LocationSettings(
              accuracy: acc,
              timeLimit: const Duration(seconds: 12),
            ),
          );
          if (pos != null) break;
        } catch (_) {}
      }
      pos ??= await Geolocator.getLastKnownPosition();
      if (pos == null) {
        setState(() => gpsStatus = 'หาตำแหน่งไม่ได้ — แตะลองใหม่');
        return;
      }
      final p = pos;
      setState(() {
        gps = p;
        gpsOk = true;
        gpsStatus = '±${p.accuracy.round()} ม.';
      });
    } catch (e) {
      setState(() => gpsStatus = 'หาตำแหน่งไม่ได้ — แตะลองใหม่');
    }
  }

  Future<void> _loadActive() async {
    setState(() {
      loadingActive = true;
      selectedIdx = -1;
    });
    try {
      final res = await apiCall('getActiveClockIns', {
        'otDate': _dateStr(otDate),
        'recorderId': (currentUser?['employee_id'] ?? '').toString(),
      });
      final data = (res['data'] as List? ?? [])
          .map((e) => Map<String, dynamic>.from(e))
          .toList();
      setState(() {
        activeList = data;
        loadingActive = false;
      });
    } catch (e) {
      setState(() {
        activeList = [];
        loadingActive = false;
        error = 'โหลดรายชื่อไม่สำเร็จ: $e';
      });
    }
  }

  Future<void> _pickPhoto() async {
    final now = DateTime.now();
    if (demoMode) {
      setState(() {
        photoBase64 = _demoPhoto;
        photoSource = 'demo';
        photoTimestamp =
            '${now.day.toString().padLeft(2, '0')}/${now.month.toString().padLeft(2, '0')}/${now.year} '
            '${now.hour.toString().padLeft(2, '0')}:${now.minute.toString().padLeft(2, '0')}:${now.second.toString().padLeft(2, '0')}';
        error = '';
      });
      return;
    }

    final picker = ImagePicker();
    // เว็บไม่รองรับบังคับกล้องหน้า — ใส่ option นี้เฉพาะตอนเป็นแอปมือถือ
    final file = kIsWeb
        ? await picker.pickImage(
            source: ImageSource.camera,
            maxWidth: 1280,
            imageQuality: 85)
        : await picker.pickImage(
            source: ImageSource.camera,
            preferredCameraDevice: CameraDevice.front,
            maxWidth: 1280,
            imageQuality: 85);
    if (file == null) return;

    final bytes = await file.readAsBytes();
    final t = DateTime.now();
    setState(() {
      photoBase64 = 'data:image/jpeg;base64,${base64Encode(bytes)}';
      photoSource = 'camera';
      photoTimestamp =
          '${t.day.toString().padLeft(2, '0')}/${t.month.toString().padLeft(2, '0')}/${t.year} '
          '${t.hour.toString().padLeft(2, '0')}:${t.minute.toString().padLeft(2, '0')}:${t.second.toString().padLeft(2, '0')}';
      error = '';
    });
    if (gps == null) _startGps();
  }

  // จำนวนนาทีที่ทำงาน (ใช้คำนวณทั้ง hoursText และเบี้ยเลี้ยง)
  int? get totalMinutes {
    final p = picked;
    if (p == null) return null;
    final parts = (p['startTime'] as String).split(':');
    var startMin = int.parse(parts[0]) * 60 + int.parse(parts[1]);
    var endMin = time.hour * 60 + time.minute;
    if (endMin <= startMin) endMin += 24 * 60;
    return endMin - startMin;
  }

  String? get hoursText {
    final total = totalMinutes;
    if (total == null) return null;
    final h = total ~/ 60, m = total % 60;
    if (h == 0) return '$m นาที';
    if (m == 0) return '$h ชม.';
    return '$h ชม. $m นาที';
  }

  // ── เงื่อนไขเบี้ยเลี้ยง (เฉพาะบริษัท 3E Innovation) ──
  //   ออกหน้างาน (field)   → ได้ 80 บาทเสมอ ไม่กำหนดเวลา
  //   รับเบี้ยเลี้ยง (normal) → ต้องทำงาน ≥ 3 ชม. ถึงได้ 80 บาท
  static const int allowanceBaht = 80;
  static const int allowanceMinHours = 3;

  bool get allowanceEligible {
    if (!showWorktype || worktype.isEmpty) return false;
    if (worktype == 'field') return true; // ออกหน้างาน — ได้เลย
    return (totalMinutes ?? 0) >= allowanceMinHours * 60; // รับเบี้ยเลี้ยง ≥3ชม.
  }

  int get allowanceAmount => allowanceEligible ? allowanceBaht : 0;

  // ข้อความที่จะบันทึกลงชีต (คอลัมน์เบี้ยเลี้ยง)
  String _allowanceLabel() {
    if (!showWorktype || worktype.isEmpty) return '';
    if (worktype == 'field') {
      return 'เบี้ยเลี้ยงออกหน้างาน $allowanceBaht บาท';
    }
    return allowanceEligible
        ? 'รับเบี้ยเลี้ยง $allowanceBaht บาท'
        : 'ไม่ได้รับเบี้ยเลี้ยง';
  }

  Future<void> _submit() async {
    setState(() => error = '');
    if (photoBase64 == null) {
      setState(() => error = 'กรุณาถ่ายรูปยืนยันก่อน');
      return;
    }
    if (gps == null) {
      setState(() => error = 'ยังไม่มีพิกัด GPS — แตะป้าย GPS เพื่อลองใหม่');
      return;
    }
    final gpsCoords =
        '${gps!.latitude.toStringAsFixed(6)}, ${gps!.longitude.toStringAsFixed(6)}';
    final mapsUrl =
        'https://maps.google.com/?q=${gps!.latitude},${gps!.longitude}';

    Map<String, dynamic> data;
    String action;
    if (isClockOut) {
      final p = picked;
      if (p == null) {
        setState(() => error = 'กรุณาเลือกชื่อพนักงาน');
        return;
      }
      if (showWorktype && worktype.isEmpty) {
        setState(() => error = 'กรุณาเลือกประเภทเบี้ยเลี้ยง');
        return;
      }
      action = 'clockOut';
      data = {
        'id': p['id'],
        'employeeName': p['employeeName'],
        'otDate': p['otDate'],
        'endTime': _timeStr(time),
        'recorderId': (currentUser?['employee_id'] ?? '').toString(),
        'workDetail': '',
        'allowance': _allowanceLabel(),
        'gpsCoords': gpsCoords,
        'address': mapsUrl,
        'selfieBase64': photoBase64,
        'photoTimestamp': photoTimestamp,
        'photoSource': photoSource,
      };
    } else {
      if (nameCtrl.text.trim().isEmpty) {
        setState(() => error = 'กรุณากรอกชื่อพนักงาน');
        return;
      }
      if (supervisorCtrl.text.trim().isEmpty) {
        setState(() => error = 'กรุณากรอกชื่อหัวหน้า');
        return;
      }
      if (company.isEmpty) {
        setState(() => error = 'กรุณาเลือกบริษัท');
        return;
      }
      action = 'clockIn';
      data = {
        'otDate': _dateStr(otDate),
        'employeeName': nameCtrl.text.trim(),
        'supervisorName': supervisorCtrl.text.trim(),
        'company': company,
        'department': department,
        'recorderId': (currentUser?['employee_id'] ?? '').toString(),
        'startTime': _timeStr(time),
        'workDetail': detailCtrl.text.trim(),
        'allowance': '',
        'gpsCoords': gpsCoords,
        'address': mapsUrl,
        'selfieBase64': photoBase64,
        'photoTimestamp': photoTimestamp,
        'photoSource': photoSource,
      };
    }

    setState(() => busy = true);
    try {
      final res = await apiCall(action, data);
      setState(() => busy = false);
      if (res['success'] == true) {
        if (!mounted) return;
        await showCupertinoDialog(
          context: context,
          builder: (_) => CupertinoAlertDialog(
            title: Text(isClockOut ? 'เลิกงานสำเร็จ' : 'เริ่มงานแล้ว'),
            content: Padding(
              padding: const EdgeInsets.only(top: 6),
              child: Text(isClockOut
                  ? 'บันทึกเรียบร้อย\nรวมเวลา ${res['hours'] ?? hoursText ?? ''}'
                  : 'บันทึกเรียบร้อย\nกลับมากด "เลิกงาน" เมื่อทำเสร็จ'),
            ),
            actions: [
              CupertinoDialogAction(
                isDefaultAction: true,
                onPressed: () => Navigator.pop(context),
                child: const Text('ตกลง'),
              ),
            ],
          ),
        );
        if (mounted) Navigator.pop(context);
      } else {
        setState(
            () => error = 'บันทึกไม่สำเร็จ: ${res['message'] ?? 'ลองใหม่'}');
      }
    } catch (e) {
      setState(() {
        busy = false;
        error = 'บันทึกไม่สำเร็จ: $e';
      });
    }
  }

  void _showSheet(Widget child, {double height = 300}) {
    showCupertinoModalPopup(
      context: context,
      builder: (_) => Container(
        height: height,
        decoration: const BoxDecoration(
          color: CupertinoColors.white,
          borderRadius: BorderRadius.vertical(top: Radius.circular(20)),
        ),
        child: SafeArea(
          top: false,
          child: Column(
            children: [
              Container(
                decoration: const BoxDecoration(
                  border: Border(
                      bottom:
                          BorderSide(color: Color(0xFFE5E9F2), width: 0.5)),
                ),
                child: Row(
                  mainAxisAlignment: MainAxisAlignment.end,
                  children: [
                    CupertinoButton(
                      padding: const EdgeInsets.symmetric(
                          horizontal: 16, vertical: 10),
                      onPressed: () => Navigator.pop(context),
                      child: const Text('เสร็จสิ้น',
                          style: TextStyle(
                              fontWeight: FontWeight.w600, color: tOrange)),
                    ),
                  ],
                ),
              ),
              Expanded(child: child),
            ],
          ),
        ),
      ),
    );
  }

  void _pickDate() => _showSheet(CupertinoDatePicker(
        mode: CupertinoDatePickerMode.date,
        initialDateTime: otDate,
        minimumDate: DateTime(2024),
        maximumDate: DateTime(2030),
        onDateTimeChanged: (d) {
          setState(() => otDate = d);
          if (isClockOut) _loadActive();
        },
      ));

  void _pickTime() => _showSheet(CupertinoDatePicker(
        mode: CupertinoDatePickerMode.time,
        use24hFormat: true,
        initialDateTime: time,
        onDateTimeChanged: (t) => setState(() => time = t),
      ));

  void _pickCompany() {
    const placeholder = 'เลือกบริษัท';
    final items = [placeholder, ...companies];
    _showSheet(CupertinoPicker(
      itemExtent: 38,
      scrollController: FixedExtentScrollController(
          initialItem: company.isEmpty ? 0 : companies.indexOf(company) + 1),
      onSelectedItemChanged: (i) => setState(() {
        company = i == 0 ? '' : companies[i - 1];
        worktype = '';
      }),
      children: items
          .map((c) => Center(
              child: Text(c,
                  style: TextStyle(
                      fontSize: 19,
                      color: c == placeholder
                          ? const Color(0xFFAEB6C6)
                          : tText))))
          .toList(),
    ));
  }

  void _pickEmployee() {
    if (activeList.isEmpty) return;
    _showSheet(CupertinoPicker(
      itemExtent: 38,
      scrollController: FixedExtentScrollController(
          initialItem: selectedIdx < 0 ? 0 : selectedIdx),
      onSelectedItemChanged: (i) => setState(() {
        selectedIdx = i;
        worktype = '';
      }),
      children: activeList
          .map((p) => Center(
              child: Text('${p['employeeName']} · ${p['startTime']}',
                  style: const TextStyle(fontSize: 17))))
          .toList(),
    ));
    if (selectedIdx < 0) setState(() => selectedIdx = 0);
  }

  @override
  Widget build(BuildContext context) {
    final routeAnim =
        ModalRoute.of(context)?.animation ?? kAlwaysCompleteAnimation;
    return CupertinoPageScaffold(
      child: Column(
        children: [
          _header(context, routeAnim),
          Expanded(
            child: AnimatedBuilder(
              animation: routeAnim,
              builder: (context, child) {
                final popping = routeAnim.status == AnimationStatus.reverse;
                final t = popping
                    ? 1.0
                    : const Interval(0.12, 1.0, curve: kSmooth)
                        .transform(routeAnim.value.clamp(0.0, 1.0));
                return Opacity(
                  opacity: t,
                  child: Transform.translate(
                    offset: Offset(0, (1 - t) * 26),
                    child: child,
                  ),
                );
              },
              child: LayoutBuilder(builder: (context, c) {
              final wide = c.maxWidth >= kWide;
              if (!wide) {
                return ListView(
                  padding: const EdgeInsets.fromLTRB(20, 20, 20, 32),
                  children: [..._infoCards(), ..._photoAndSubmit()],
                );
              }
              return SingleChildScrollView(
                padding: const EdgeInsets.symmetric(vertical: 24),
                child: Center(
                  child: ConstrainedBox(
                    constraints: const BoxConstraints(maxWidth: 1000),
                    child: Padding(
                      padding: const EdgeInsets.symmetric(horizontal: 20),
                      child: Row(
                        crossAxisAlignment: CrossAxisAlignment.start,
                        children: [
                          Expanded(
                              flex: 11,
                              child: Column(children: _infoCards())),
                          const SizedBox(width: 24),
                          Expanded(
                              flex: 9,
                              child: Column(children: _photoAndSubmit())),
                        ],
                      ),
                    ),
                  ),
                ),
              );
            }),
            ),
          ),
        ],
      ),
    );
  }

  Widget _header(BuildContext context, Animation<double> routeAnim) {
    return AnimatedBuilder(
      animation: routeAnim,
      builder: (context, child) {
        final popping = routeAnim.status == AnimationStatus.reverse;
        final t = popping ? 1.0 : kSmooth.transform(routeAnim.value.clamp(0.0, 1.0));
        final extra = 300.0 * (1 - t);
        final radius = 24.0 + 8.0 * (1 - t);
        return Container(
          width: double.infinity,
          decoration: BoxDecoration(
            gradient: _headGrad,
            borderRadius:
                BorderRadius.vertical(bottom: Radius.circular(radius)),
          ),
          child: Column(
            mainAxisSize: MainAxisSize.min,
            children: [child!, SizedBox(height: extra)],
          ),
        );
      },
      child: SafeArea(
        bottom: false,
        child: Padding(
          padding: const EdgeInsets.fromLTRB(8, 6, 16, 16),
          child: Stack(
            alignment: Alignment.center,
            children: [
              Align(
                alignment: Alignment.center,
                child: Text(
                  isClockOut ? 'เลิกงาน OT' : 'เริ่มงาน OT',
                  style: const TextStyle(
                      fontSize: 19,
                      fontWeight: FontWeight.w700,
                      color: CupertinoColors.white),
                ),
              ),
              Align(
                alignment: Alignment.centerLeft,
                child: CupertinoButton(
                  padding: const EdgeInsets.all(8),
                  onPressed: () => Navigator.pop(context),
                  child: const Icon(Icons.arrow_back_ios_new_rounded,
                      color: CupertinoColors.white, size: 26),
                ),
              ),
              Align(
                alignment: Alignment.centerRight,
                child: GestureDetector(
                  onTap: _startGps,
                  child: Container(
                    padding: const EdgeInsets.symmetric(
                        horizontal: 12, vertical: 6),
                    decoration: BoxDecoration(
                      color: const Color(0x2EFFFFFF),
                      borderRadius: BorderRadius.circular(99),
                      border: Border.all(color: const Color(0x4DFFFFFF)),
                    ),
                    child: Row(
                      mainAxisSize: MainAxisSize.min,
                      children: [
                        Icon(
                            gpsOk
                                ? Icons.my_location_rounded
                                : Icons.location_searching_rounded,
                            size: 13,
                            color: gpsOk
                                ? const Color(0xFF8EF0B0)
                                : const Color(0xFFFFD56A)),
                        const SizedBox(width: 5),
                        Text(gpsStatus,
                            style: TextStyle(
                                fontSize: 12,
                                color: gpsOk
                                    ? const Color(0xFF8EF0B0)
                                    : const Color(0xFFFFD56A))),
                      ],
                    ),
                  ),
                ),
              ),
            ],
          ),
        ),
      ),
    );
  }

  Widget _card({required String title, required List<Widget> children}) {
    return Container(
      width: double.infinity,
      margin: const EdgeInsets.only(bottom: 16),
      padding: const EdgeInsets.all(18),
      decoration: BoxDecoration(
        color: CupertinoColors.white,
        borderRadius: BorderRadius.circular(16),
        border: Border.all(color: tCreamLine),
        boxShadow: const [
          BoxShadow(
              color: Color(0x0D0F172A), blurRadius: 12, offset: Offset(0, 4)),
        ],
      ),
      child: Column(
        crossAxisAlignment: CrossAxisAlignment.start,
        children: [
          Row(
            children: [
              Container(
                  width: 3.5,
                  height: 16,
                  decoration: BoxDecoration(
                      color: tGold,
                      borderRadius: BorderRadius.circular(2))),
              const SizedBox(width: 8),
              Text(title,
                  style: const TextStyle(
                      fontSize: 15.5,
                      fontWeight: FontWeight.w700,
                      color: tDark)),
            ],
          ),
          const SizedBox(height: 14),
          ...children,
        ],
      ),
    );
  }

  Widget _fieldBox({
    required String label,
    required Widget child,
    VoidCallback? onTap,
    bool chevron = false,
  }) {
    final box = Container(
      width: double.infinity,
      margin: const EdgeInsets.only(bottom: 10),
      padding: const EdgeInsets.symmetric(horizontal: 14, vertical: 10),
      decoration: BoxDecoration(
        color: tField,
        borderRadius: BorderRadius.circular(12),
        border: Border.all(color: const Color(0xFFF8F5EF)),
      ),
      child: Row(
        children: [
          Expanded(
            child: Column(
              crossAxisAlignment: CrossAxisAlignment.start,
              children: [
                Text(label,
                    style: const TextStyle(fontSize: 12, color: tText2)),
                const SizedBox(height: 2),
                child,
              ],
            ),
          ),
          if (chevron)
            const Icon(Icons.keyboard_arrow_down_rounded,
                size: 15, color: tText2),
        ],
      ),
    );
    return onTap == null ? box : GestureDetector(onTap: onTap, child: box);
  }

  Widget _valueText(String v, {Color color = tText, FontWeight w = FontWeight.w600}) =>
      Text(v, style: TextStyle(fontSize: 16, fontWeight: w, color: color));

  Widget _textField(TextEditingController ctrl, String placeholder,
      {int maxLines = 1}) {
    return CupertinoTextField(
      controller: ctrl,
      placeholder: placeholder,
      maxLines: maxLines,
      padding: EdgeInsets.zero,
      style: const TextStyle(
          fontSize: 16, fontWeight: FontWeight.w600, color: tText),
      placeholderStyle: const TextStyle(
          fontSize: 16, color: Color(0xFFAEB6C6), fontWeight: FontWeight.w400),
      decoration: const BoxDecoration(color: Color(0x00000000)),
    );
  }

  List<Widget> _infoCards() => [
        _card(
          title: 'ข้อมูลพนักงาน',
          children: [
            _fieldBox(
              label: 'วันที่',
              chevron: true,
              onTap: _pickDate,
              child: _valueText(_dateThai(otDate)),
            ),
            if (!isClockOut) ...[
              _fieldBox(
                  label: 'ชื่อพนักงาน',
                  child: _textField(nameCtrl, 'ชื่อ - นามสกุล')),
              _fieldBox(
                  label: 'หัวหน้า',
                  child: _textField(supervisorCtrl, 'ชื่อหัวหน้า')),
              _fieldBox(
                label: 'บริษัท',
                chevron: true,
                onTap: _pickCompany,
                child: _valueText(company.isEmpty ? 'แตะเพื่อเลือก' : company,
                    color: company.isEmpty ? const Color(0xFFAEB6C6) : tText,
                    w: company.isEmpty ? FontWeight.w400 : FontWeight.w600),
              ),
            ] else ...[
              _fieldBox(
                label: 'พนักงาน',
                chevron: true,
                onTap: _pickEmployee,
                child: loadingActive
                    ? const CupertinoActivityIndicator()
                    : _valueText(
                        activeList.isEmpty
                            ? 'ไม่มีคนเริ่มงาน'
                            : (picked == null
                                ? 'แตะเพื่อเลือก'
                                : '${picked!['employeeName']}'),
                        color: picked == null
                            ? const Color(0xFFAEB6C6)
                            : tText,
                        w: picked == null
                            ? FontWeight.w400
                            : FontWeight.w600),
              ),
              if (picked != null)
                _fieldBox(
                  label: 'เริ่มงานไว้เมื่อ',
                  child: _valueText('${picked!['startTime']} น.',
                      color: tSage, w: FontWeight.w700),
                ),
            ],
            _fieldBox(
              label: isClockOut ? 'เวลาเลิกงาน' : 'เวลาเริ่มงาน',
              chevron: true,
              onTap: _pickTime,
              child: _valueText('${_timeStr(time)} น.',
                  color: tBlueG, w: FontWeight.w700),
            ),
            if (isClockOut && hoursText != null)
              _fieldBox(
                label: 'เวลารวม',
                child: _valueText(hoursText!,
                    color: tGold, w: FontWeight.w700),
              ),
          ],
        ),
        if (isClockOut && showWorktype)
          _card(
            title: 'ประเภทเบี้ยเลี้ยง',
            children: [
              Row(
                children: [
                  Expanded(
                      child: _chip('💵 รับเบี้ยเลี้ยง', 'normal')),
                  const SizedBox(width: 10),
                  Expanded(child: _chip('🚗 ออกหน้างาน', 'field')),
                ],
              ),
            ],
          ),
        if (!isClockOut)
          _card(
            title: 'รายละเอียดงาน',
            children: [
              _fieldBox(
                label: 'งานที่ทำในช่วง OT',
                child: _textField(detailCtrl, 'อธิบายงานที่ทำ...',
                    maxLines: 3),
              ),
            ],
          ),
      ];

  Widget _chip(String text, String value) {
    final on = worktype == value;
    return GestureDetector(
      onTap: () => setState(() => worktype = value),
      child: Container(
        padding: const EdgeInsets.symmetric(vertical: 12),
        alignment: Alignment.center,
        decoration: BoxDecoration(
          color: on ? accent : tField,
          borderRadius: BorderRadius.circular(12),
          border: Border.all(color: on ? accent : const Color(0xFFF8F5EF)),
        ),
        child: Text(text,
            style: TextStyle(
                fontSize: 14.5,
                fontWeight: on ? FontWeight.w700 : FontWeight.w400,
                color: on ? CupertinoColors.white : tText)),
      ),
    );
  }

  List<Widget> _photoAndSubmit() => [
        _card(
          title: 'ยืนยันตัวตน',
          children: [
            if (photoBase64 == null)
              GestureDetector(
                onTap: _pickPhoto,
                child: Container(
                  width: double.infinity,
                  padding: const EdgeInsets.symmetric(vertical: 28),
                  decoration: BoxDecoration(
                    color: tOrangeSoft,
                    borderRadius: BorderRadius.circular(14),
                    border: Border.all(color: const Color(0xFFE4D9BD)),
                  ),
                  child: Column(
                    children: [
                      Container(
                        width: 60,
                        height: 60,
                        decoration: BoxDecoration(
                            color: accent, shape: BoxShape.circle),
                        child: const Icon(Icons.photo_camera_rounded,
                            color: CupertinoColors.white, size: 28),
                      ),
                      const SizedBox(height: 10),
                      Text('ถ่ายรูปยืนยันตัวตน',
                          style: TextStyle(
                              fontSize: 15.5,
                              fontWeight: FontWeight.w700,
                              color: accent)),
                      const Text('ต้องถ่ายรูปสดเท่านั้น',
                          style:
                              TextStyle(fontSize: 12.5, color: tText2)),
                    ],
                  ),
                ),
              )
            else
              Column(
                children: [
                  ClipRRect(
                    borderRadius: BorderRadius.circular(12),
                    child: Image.memory(
                      base64Decode(photoBase64!.split(',').last),
                      height: 280,
                      width: double.infinity,
                      fit: BoxFit.cover,
                    ),
                  ),
                  const SizedBox(height: 8),
                  Text('📸 ถ่ายสด · $photoTimestamp',
                      style:
                          const TextStyle(fontSize: 12, color: tText2)),
                  CupertinoButton(
                    padding: const EdgeInsets.symmetric(vertical: 6),
                    onPressed: () {
                      setState(() => photoBase64 = null);
                      _pickPhoto();
                    },
                    child: Text('ถ่ายใหม่',
                        style: TextStyle(
                            color: accent, fontWeight: FontWeight.w600)),
                  ),
                ],
              ),
          ],
        ),
        if (error.isNotEmpty)
          Padding(
            padding: const EdgeInsets.only(bottom: 10),
            child: Row(
              children: [
                const Icon(Icons.error_rounded,
                    size: 16, color: tRed),
                const SizedBox(width: 6),
                Expanded(
                  child: Text(error,
                      style:
                          const TextStyle(color: tRed, fontSize: 13)),
                ),
              ],
            ),
          ),
        GestureDetector(
          onTap: busy ? null : _submit,
          child: Container(
            width: double.infinity,
            padding: const EdgeInsets.symmetric(vertical: 15),
            alignment: Alignment.center,
            decoration: BoxDecoration(
              gradient: btnGrad,
              borderRadius: BorderRadius.circular(14),
              boxShadow: [
                BoxShadow(
                    color: accent.withOpacity(0.35),
                    blurRadius: 16,
                    offset: const Offset(0, 6)),
              ],
            ),
            child: busy
                ? const CupertinoActivityIndicator(
                    color: CupertinoColors.white)
                : Text(isClockOut ? 'บันทึกเลิกงาน' : 'เริ่มงาน OT',
                    style: const TextStyle(
                        fontSize: 17,
                        fontWeight: FontWeight.w700,
                        color: CupertinoColors.white)),
          ),
        ),
      ];
}
