##################################################
# Makefile of pmtestx.asm (x=[1,2,3...])
##################################################

SRC:=pmtest2.asm
BIN:=$(subst .asm,.com,$(SRC))
DEP:=pm.img.gz freedos.img.gz

.PHONY : run init move debug clean

$(BIN) : $(SRC)
	nasm $< -o $@

init: $(DEP)
	gzip -cd pm.img.gz > pm.img
	gzip -cd freedos.img.gz > freedos.img

move: $(BIN)
	sudo mount -o loop pm.img /mnt
	sudo cp $(BIN) /mnt -v
	sudo umount /mnt

run : move
	qemu-system-i386 -fda freedos.img -fdb pm.img -boot a

clean: 
	rm -f $(BIN)