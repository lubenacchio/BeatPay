# BeatPay
from flask import Flask, render_template, request, redirect, session
import os
app = Flask(__name__)
app.secret_key = os.urandom(24)  # Clave secreta para la sesión
@app.route('/')
def home():
    if 'username' in session:
        return 'Bienvenido, ' + session['username']
    else:
        return redirect('/login')

@app.route('/login', methods=['GET', 'POST'])
def login():
    if request.method == 'POST':
        username = request.form['username']
        password = request.form['password']
        # Verificar las credenciales del usuario (ejemplo: consultar una base de datos)
        # Si las credenciales son válidas, establecer la sesión del usuario
        session['username'] = username
        return redirect('/')
    return render_template('login.html')

@app.route('/logout')
def logout():
    session.pop('username', None)
    return redirect('/')
<h2>Iniciar sesión</h2>
<form method="POST" action="/login">
    <input type="text" name="username" placeholder="Nombre de usuario" required><br>
    <input type="password" name="password" placeholder="Contraseña" required><br>
    <input type="submit" value="Iniciar sesión">
</form>
if __name__ == '__main__':
    app.run(debug=True)
