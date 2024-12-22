# SOLID-Principles-1-Single-Responsibility-Principle-SRP-



from pathlib import Path
from zipfile import ZipFile
class FileManager:
  def __init__(self, filename):
    self.path = Path(filename)
  def read(self, encoding="utf-8"):
    return self.path.read_text(encoding)
  def write(self, data, encoding="utf-8"):
    self.path.write_text(data, encoding)
  def compress(self):
    with ZipFile(self.path.with_suffix(".zip"), mode="w") as     archive:
    archive.write(self.path)
  def decompress(self):
  with ZipFile(self.path.with_suffix(".zip"), mode="r")

#In this example, your FileManager class has two different responsibilities. It usesthe .read() and .write() methods to manage the file. It also deals with ZIParchives by providing the .compress() and .decompress() methods.
#This class violates the single-responsibility principle because it has two reasons forchanging its internal implementation. 
#To fix this issue and make your design morerobust, you can split the class into two smaller, more focused classes, each with its own specific concern:

#the fixed code will be  :
from pathlib import Path
from zipfile import ZipFile
class FileManager :
  def __init__(self, filename):
    self.path = Path(filename)
  def read(self, encoding="utf-8"):
    return self.path.read_text(encoding)
  def write(self, data, encoding="utf-8"):
    self.path.write_text(data, encoding)
class ZipFileManager:
  def __init__(self, filename):
    self.path = Path(filename)
  def compress(self):with ZipFile(self.path.with_suffix(".zip"), mode="w") as archive:
    archive.write(self.path)
  def decompress(self):
    with ZipFile(self.path.with_suffix(".zip"), mode="r") as archive:
    archive.extractall()

