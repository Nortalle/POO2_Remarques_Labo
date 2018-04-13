# Labo1 - Matrice

## Exemple 1

### Erreur

```c++
int main(int argc, char** argv)
```

### Remarque

Si les arguments ne sont pas utilisés dans le labo, ne pas les mettre

### Solution

```c++
int main()
```



## Exemple 2

### Erreur

```

```

### Remarque

### Solution

## Exemple 3

### Erreur

```

```

### Remarque

### Solution

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
String Strin::operator+(const String &other){
    String newString(this->value); // value est l'attribut char* de notre String
    newString.append(other);
    return newString;
}
```

### Remarque

Il y a mieux à faire

### Solution

```c++
String Strin::operator+(const String &other){
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

Si `value == string`vous perdez les données. C'est comme un opérateur d'affectation, il faut vérifier que le paramètre ne soit pas l'objet courant

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

