SRCS=main.c memory_controller.c
OBJS=$(addprefix $(OUT_DIR)/, $(patsubst %.c, %.o, $(SRCS)))
# Make this to the prefix of your target files. EX: scheduler
NAME_RULE="scheduler*.c"
TARGETS=$(shell ls "./$(NAME_RULE)" | awk '{print $$1}' | sed -e 's/\.c//g') 

# Choose your directories
SRC_DIR=./
OUT_DIR=../obj
OUT_BIN_DIR=../bin
ifndef CAPN
	CAPN=1
endif
ifndef PWRN
	PWRN=1
endif
ifndef MARKING_CAP
	MARKING_CAP=20
endif


CFLAGS=-O2 -std=c99 -Wall
green=\033[1;32m
NC=\033[0m # No Color

all	:	$(TARGETS)

# TODO Make it your own testing configuration, scheduler-fcfs is the name of your scheduler. Revise it to your program!!!!!
# TODO 請把":"後面的scheduler-fcfs換成你自己的程式
execute	:	scheduler-parbs
	@echo -e "\nExecuting script $(green)../runsim$(NC)\n"
	@cd ../ && ./runsim
	@echo -e "\nExecuting script $(green)../parse.perl$(NC)\n"
	@cd ../ && ./parse.perl

# General make
$(TARGETS)	:	$(OBJS) 
	@echo -e "building $(green)$@$(NC)"
	@mkdir -p $(OUT_BIN_DIR)
	$(CC) $(CFLAGS) -o $(OUT_BIN_DIR)/$@ $(OBJS) $@.c

# Make yours if you define variables which is conflict with others or you want to name by your-self. 
scheduler-frfcfs	:	$(OBJS)
	@echo -e "building $(green)$@$(NC)"
	@mkdir -p $(OUT_BIN_DIR)
	$(CC) $(CFLAGS) -DCAPN=$(CAPN) -o $(OUT_BIN_DIR)/$@-$(CAPN) $(OBJS) $@.c

scheduler-pwrdn	:	$(OBJS)
	@echo -e "building $(green)$@$(NC)"
	@mkdir -p $(OUT_BIN_DIR)
	$(CC) $(CFLAGS) -DPWRN=$(PWRN) -o $(OUT_BIN_DIR)/$@-$(PWRN) $(OBJS) $@.c

scheduler-parbs	:	$(OBJS)
	@echo -e "building $(green)$@$(NC)"
	@mkdir -p $(OUT_BIN_DIR)
	$(CC) $(CFLAGS) -DMARKING_CAP=$(MARKING_CAP) -o $(OUT_BIN_DIR)/$@-$(MARKING_CAP) $(OBJS) $@.c

$(OUT_DIR)/%.o	:	%.c
	@mkdir -p $(@D)
	$(CC) $(CFLAGS) -c $< -o $@

clean	:
	rm -rf $(OUT_DIR) $(OUT_BIN_DIR)

