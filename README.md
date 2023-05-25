# 7d-Cistercian-Lattice-Using-colours
7d Cistercian Lattice using colours
//

#include <iostream>
#include <vector>

using namespace std;

// This function creates a 4D color matrix.
vector<vector<vector<vector<unsigned char>>>> createColorMatrix(int width, int height, int depth, int channels) {
  vector<vector<vector<vector<unsigned char>>>> matrix(width, vector<vector<vector<unsigned char>>>(height, vector<vector<unsigned char>>(depth, vector<unsigned char>(channels))));

  // Fill the matrix with random colors.
  for (int i = 0; i < width; i++) {
    for (int j = 0; j < height; j++) {
      for (int k = 0; k < depth; k++) {
        for (int l = 0; l < channels; l++) {
          matrix[i][j][k][l] = rand() % 256;
        }
      }
    }
  }

  return matrix;
}

// This function encrypts a message using the 4D color matrix.
string encryptMessage(const string& message, const vector<vector<vector<vector<unsigned char>>>>& matrix) {
  // Convert the message to a sequence of bytes.
  vector<unsigned char> bytes(message.begin(), message.end());

  // Encrypt the bytes using the 4D color matrix.
  for (int i = 0; i < bytes.size(); i++) {
    bytes[i] = matrix[bytes[i] % matrix.size()][bytes[i] / matrix.size()][bytes[i] / matrix.size() / matrix.size()][bytes[i] / matrix.size() / matrix.size() / matrix.size()];
  }

  // Convert the encrypted bytes back to a string.
  return string((char*)bytes.data(), bytes.size());
}

// This function decrypts a message that was encrypted using the 4D color matrix.
string decryptMessage(const string& encryptedMessage, const vector<vector<vector<vector<unsigned char>>>>& matrix) {
  // Convert the encrypted message to a sequence of bytes.
  vector<unsigned char> bytes(encryptedMessage.begin(), encryptedMessage.end());

  // Decrypt the bytes using the 4D color matrix.
  for (int i = 0; i < bytes.size(); i++) {
    bytes[i] = matrix[bytes[i] % matrix.size()][bytes[i] / matrix.size()][bytes[i] / matrix.size() / matrix.size()][bytes[i] / matrix.size() / matrix.size() / matrix.size()];
  }

  // Convert the decrypted bytes back to a string.
  return string((char*)bytes.data(), bytes.size());
}

int main() {
  // Create a 4D color matrix.
  const int width = 100;
  const int height = 100;
  const int depth = 100;
  const int channels = 3;
  vector<vector<vector<vector<unsigned char>>>> matrix = createColorMatrix(width, height, depth, channels);

  // Encrypt a message.
  string message = "This is a secret message.";
  string encryptedMessage = encryptMessage(message, matrix);

  // Decrypt the message.
  string decryptedMessage = decryptMessage(encryptedMessage, matrix);

  // Print the encrypted and decrypted messages.
  cout << "Encrypted message: " << encryptedMessage << endl;
  cout << "Decrypted message: " << decryptedMessage << endl;

  return 0;
}
