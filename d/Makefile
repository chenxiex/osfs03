##################################################
# Makefile of pmtestx.asm (x=[1,2,3...])
##################################################

SRC:=pmtest4.asm
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

debug: move
	tmux new-session -d -s debug_session 'qemu-system-i386 -fda freedos.img -fdb pm.img -boot a -s -S -monitor stdio'
	tmux split-window -h -t debug_session 'gdb -x gdbinit'
	tmux attach -t debug_session

clean: 
	rm -f $(BIN)