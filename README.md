import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Calculadora',
      theme: ThemeData(primarySwatch: Colors.blue),
      home: Calculadora(),
    );
  }
}

class Calculadora extends StatefulWidget {
  @override
  _CalculadoraState createState() => _CalculadoraState();
}

class _CalculadoraState extends State<Calculadora> {
  String resultado = "";
  String operacao = "";
  String anterior = "";

  void buttonPressed(String buttonText) {
    setState(() {
      if (buttonText == "C") {
        resultado = "";
        operacao = "";
        anterior = "";
      } else if (buttonText == "=") {
        if (operacao == "+") {
          resultado = (double.parse(anterior) + double.parse(resultado)).toString();
        } else if (operacao == "-") {
          resultado = (double.parse(anterior) - double.parse(resultado)).toString();
        } else if (operacao == "*") {
          resultado = (double.parse(anterior) * double.parse(resultado)).toString();
        } else if (operacao == "/") {
          resultado = (double.parse(anterior) / double.parse(resultado)).toString();
        }
        operacao = "";
        anterior = "";
      } else if (buttonText == "+" || buttonText == "-" || buttonText == "*" || buttonText == "/") {
        operacao = buttonText;
        anterior = resultado;
        resultado = "";
      } else {
        resultado += buttonText;
      }
    });
  }

  Widget buildButton(String buttonText) {
    return Expanded(
      child: Padding(
        padding: const EdgeInsets.all(8.0),
        child: ElevatedButton(
          style: ElevatedButton.styleFrom(
            padding: EdgeInsets.symmetric(vertical: 24),
            primary: Colors.blueAccent,
            shape: RoundedRectangleBorder(
              borderRadius: BorderRadius.circular(10),
            ),
          ),
          onPressed: () => buttonPressed(buttonText),
          child: Text(buttonText, style: TextStyle(fontSize: 24, color: Colors.white)),
        ),
      ),
    );
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("Calculadora")),
      body: Column(
        mainAxisAlignment: MainAxisAlignment.end,
        children: [
          Padding(
            padding: const EdgeInsets.all(20),
            child: Text(resultado, style: TextStyle(fontSize: 48, fontWeight: FontWeight.bold)),
          ),
          Row(
            children: [
              buildButton("7"),
              buildButton("8"),
              buildButton("9"),
              buildButton("/"),
            ],
          ),
          Row(
            children: [
              buildButton("4"),
              buildButton("5"),
              buildButton("6"),
              buildButton("*"),
            ],
          ),
          Row(
            children: [
              buildButton("1"),
              buildButton("2"),
              buildButton("3"),
              buildButton("-"),
            ],
          ),
          Row(
            children: [
              buildButton("C"),
              buildButton("0"),
              buildButton("="),
              buildButton("+"),
            ],
          ),
        ],
      ),
    );
  }
}

