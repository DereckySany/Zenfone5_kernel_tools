# Ferramentas do kernel Zenfone5

## Baixe as ferramentas toolchain 

https://android.googlesource.com/platform/prebuilts/gcc/linux-x86/x86/x86_64-linux-android-4.8/+/android-5.1.1_r13

Coloque em:

> prebuilts/gcc/linux-x86/x86/x86_64-linux-android-4.8

### 	TARGET_DEVICE=hd  (A500CG/A501CG/A600CG - default)

### Para construir o kerne a partir da fonte:
```
$ make -f KernelMakefile TARGET_DEVICE=hd build_kernel
```
OU
```
$ make -f KernelMakefile TARGET_DEVICE=hd modules_install
```

Depois de compilar o kernel a partir da fonte, é assim que você gera os arquivos .dep necessários:

`
modules.alias
modules.alias.bin
modules.builtin.bin
modules.dep
modules.dep.bin
modules.devname
modules.softdep
modules.symbols
modules.symbols.bin
`
Esse arquivo é gerado e preciso se o kernel do zenfone 5 for executado com módulos, sugiro corrigir o kernel para executar todos os módulos a serem incorporados.

- O comando precisa gerar este arquivo é beloc em seu terminal
```
make -f KernelMakefile TARGET_DEVICE=hd copy_modules_to_root
```
Após o sucesso, você encontrará todos os módulos em `out/target/product/asusctp_hd/root`

- Copie o ramdisk e comece a empacotar o kernel
```
pack ramdisk.cio.gz
```
```
find . | cpio -o -H newc | gzip > ../ramdisk.cpio.gz
```
```
pach the boot image 
```
- Comando do Teminal para empacotar:
```
pack_intel boot.img bzImage ramdisk.cpio.gz new_boot.img
```
- Comando do Teminal para descompactar:
```
unpack_intel boot.img bzImage ramdisk.cpio.gz
```
