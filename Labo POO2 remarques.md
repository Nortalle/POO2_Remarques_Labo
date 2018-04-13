# Labo1 - Matrice

## Exemple 1

### Erreur

```c++
#include "Matrix.h"
#include <iostream>
								  //1
using namespace std;

int main(int argc, char** argv) {	 //2
    Matrix m = Matrix(5);
    cout << m << "\n";				//3
    
    Matrix n = Matrix(4);
    
    try {
        m.and(n);
    } catch(std::runtime& e){		 //4
        cout << "coucou" << e.what();
    }
    
    return 0;						//5
}
```

### Remarque

Il faut inclure la librairie `stdexcept`du moment que l'on touche aux exceptions.

Si les arguments ne sont pas utilisés dans le labo, ne pas les mettre.

Il faut utiliser `endl` au lieu de `\n`.

L'exception doit être reçue en constante.

Retourner `EXIT_SUCCESS` 

### Solution

```c++
#include "Matrix.h"
#include <iostream>
#include <stdexcept>

using namespace std;

int main()) {
    Matrix m = Matrix(5);
    cout << m << endl;
    
    Matrix n = Matrix(4);
    
    try {
        m.and(n);
    } catch(const std::runtime& e){}
        cout << "coucou" << e.what();
    }
    
    return EXIT_SUCCESS;
}
```

## Exemple 2

### Erreur

```c++
Matrix(const size_t& size, const bool& randomize);
```

### Remarque

Pas besoin pour les types primitifs(Sauf si nous voulons en modifier le contenu)

### Solution

```c++
Matrix(size_t size, bool randomize);
```

## Exemple 3

### Erreur

```c++
Matrix* perform(const Operation& operation, const Matrix& m1, const Matrix& m2);

Matrix* updateAnd(const Matrix& other);

Matrix* updateXor(const Matrix& other);

Matrix* updateOr(const Matrix& other);
```

### Remarque

WHAT

### Solution

```c++
Matrix& perform(const Operation& operation, const Matrix& m1, const Matrix& m2);

Matrix& updateAnd(const Matrix& other);

Matrix& updateXor(const Matrix& other);

Matrix& updateOr(const Matrix& other);
```

# Labo2 - String

## Exemple 1

### Erreur

```c++
/**
* @return le String en chaîne de caractère
*/
char* asCharArray() const;
```

### Remarque

Ce code permet de modifier le contenu d'un String constant

### Solution

```c++
const char* asCharArray() const;
```

## Exemple 2

### Erreur

```c++
String String::operator+(const String &other){
    String newString(this->value); // value est l'attribut char* de notre String
    newString.append(other);
    return newString;
}
```

### Remarque

Il y a mieux à faire

### Solution

```c++
String String::operator+(const String &other){
	return String(*this).append(other);
}
```



## Exemple 3

### Erreur

```c++
static const char* DOUBLE_FORMAT = "%f"
```

### Remarque

"1.3" donne "1.3000......"

### Solution

```c++
static const char* DOUBLE_FORMAT = "%g"
```

## Exemple 3

### Erreur

```c++
    /**
	* Remplace la chaîne de caractères du String par une autre
	*
	* @param string  : Chaîne à copier dans la String
	* @return La string sur laquelle nous avons opéré le remplacement
	*/
    String& String::replace(const char *string) throw (std::bad_alloc) {

        clearValue();
        return fill(string);
    }		 

	/**
    * Remplace la chaîne de caractères du String par celle d'une autre String
    *
	* @param string  : String à copier dans la String
    * @return La string sur laquelle nous avons opéré le remplacement
    */
    String& String::replace(const String &string) throw (std::bad_alloc) {
       clearValue();
       return fill(string.value);
	}

 	/**
    * Nettoie le contenu de cette String
    */
	void String::clearValue() {
   		size = 0;
   		delete[] value;
	}

	/**
    * Ecrase le contenu de cette string
    * @param content   Le nouveau contenu
    */
    String& String::fill(const char *content) throw (std::bad_alloc) {

    	size = strlen(content);
       	value = new char[size + 1];

       	strcpy(value, content);
       	return *this;
    }	
```

### Remarque

Dans `String::replace`, Si `value == string` vous perdez les données. C'est comme un opérateur d'affectation, il faut vérifier que le paramètre ne soit pas l'objet courant

### Solution

```c++
    String& String::replace(const char *string) throw (std::bad_alloc) {

        if(value != string) {
        	clearValue();
            fill(string);
        }
        return *this;
    }		 

    String& String::replace(const String &string) throw (std::bad_alloc) {
       return replace (string.value);
	}
```

