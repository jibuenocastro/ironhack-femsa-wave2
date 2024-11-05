Scenario 1: User Authentication Tests
    Original Test Case (Pseudocode):
    TEST UserAuthentication
        ASSERT_TRUE(authenticate("validUser", "validPass"), "Should succeed with correct credentials")
        ASSERT_FALSE(authenticate("validUser", "wrongPass"), "Should fail with wrong credentials")
    END TEST

Explicación: en este test el nombrado del test no es descriptivo a como muestra en el módulo del curso, 
adicional se están haciendo dos validaciones dentro del mismo test, lo ideal es separalos por funcionalidad de codigo que
se está probando

Lo haría de la siguiente manera:

Escenario 1:

1.-Crear un mock que simule el llamado al metodo de autenticación que sea exitoso
2.-validar la salida 

    TEST Should_Login_Successfully

        _responseMemberEntity = {
            "code": "Success"
        }

        Mock.Get(_loginApiClient)
        .Setup(
            x => x.ValidateLogin(It.IsAny<string>(), It.IsAny<string>()))
        .ReturnsAsync(_responseMemberEntity);

        var response = await _httpClient.GetAsync($"login/");


        Assert.True(response.code, "Success")
        
    END TEST

Escenario 2:
1.-Crear un mock que simule el llamado una exepcion cuando el password no sea el correcto 
2.-validar la salida 

    TEST Should_Login_failed

        _responseMemberEntity = {
            "code": "wrongPass"
        }

        Mock.Get(_loginApiClient)
        .Setup(
            x => x.ValidateLogin(It.IsAny<string>(), It.IsAny<string>()))
        .ThrowsAsync(_responseMemberEntity);

        var response = await _httpClient.GetAsync($"login/");
        Assert.False(response.code, "wrongPass")
        
    END TEST


