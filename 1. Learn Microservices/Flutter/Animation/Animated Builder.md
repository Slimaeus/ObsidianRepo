```dart
AnimatedBuilder(

        animation: _heightAnimation,

        builder: (ctx, ch) => Container(

            // height: _authMode == AuthMode.Signup ? 320 : 260,

            height: _heightAnimation.value.height,

            constraints:

                BoxConstraints(minHeight: _heightAnimation.value.height),

            width: deviceSize.width * 0.75,

            padding: EdgeInsets.all(16.0),

            child: ch),

        child: Form(

          key: _formKey,

          child: SingleChildScrollView(

            child: Column(

              children: <Widget>[

                TextFormField(

                  decoration: InputDecoration(labelText: 'E-Mail'),

                  keyboardType: TextInputType.emailAddress,

                  validator: (value) {

                    if (value.isEmpty || !value.contains('@')) {

                      return 'Invalid email!';

                    }

                    return null;

                  },

                  onSaved: (value) {

                    _authData['email'] = value;

                  },

                ),

                TextFormField(

                  decoration: InputDecoration(labelText: 'Password'),

                  obscureText: true,

                  controller: _passwordController,

                  validator: (value) {

                    if (value.isEmpty || value.length < 5) {

                      return 'Password is too short!';

                    }

                    return null;

                  },

                  onSaved: (value) {

                    _authData['password'] = value;

                  },

                ),

                if (_authMode == AuthMode.Signup)

                  TextFormField(

                    enabled: _authMode == AuthMode.Signup,

                    decoration: InputDecoration(labelText: 'Confirm Password'),

                    obscureText: true,

                    validator: _authMode == AuthMode.Signup

                        ? (value) {

                            if (value != _passwordController.text) {

                              return 'Passwords do not match!';

                            }

                            return null;

                          }

                        : null,

                  ),

                SizedBox(

                  height: 20,

                ),

                if (_isLoading)

                  CircularProgressIndicator()

                else

                  ElevatedButton(

                    child:

                        Text(_authMode == AuthMode.Login ? 'LOGIN' : 'SIGN UP'),

                    onPressed: _submit,

                    style: ButtonStyle(

                        shape: MaterialStateProperty.all(

                          RoundedRectangleBorder(

                            borderRadius: BorderRadius.circular(30),

                          ),

                        ),

                        padding: MaterialStateProperty.all(EdgeInsets.symmetric(

                            horizontal: 30.0, vertical: 8.0)),

                        backgroundColor: MaterialStateProperty.all(

                            Theme.of(context).primaryColor),

                        foregroundColor: MaterialStateProperty.all(

                            Theme.of(context).primaryTextTheme.button.color)),

                  ),

                TextButton(

                  child: Text(

                      '${_authMode == AuthMode.Login ? 'SIGNUP' : 'LOGIN'} INSTEAD',

                      style: TextStyle(

                        color: Theme.of(context).primaryColor,

                      )),

                  onPressed: _switchAuthMode,

                  style: TextButton.styleFrom(

                      padding:

                          EdgeInsets.symmetric(horizontal: 30.0, vertical: 4),

                      textStyle:

                          TextStyle(color: Theme.of(context).primaryColor),

                      tapTargetSize: MaterialTapTargetSize.shrinkWrap),

                ),

              ],

            ),

          ),

        ),

      ),
```