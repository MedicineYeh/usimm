SRCS=main.c memory_controller.c
OBJS=$(addprefix $(OUT_DIR)/, $(patsubst %.c, %.o, $(SRCS)))
# TODO : Make this to the prefix of your target files. EX: scheduler
NAME_RULE="scheduler-*.c"
TARGETS=$(shell ls "./$(NAME_RULE)" | awk '{print $$1}' | sed -e 's/\.c//g') 

# TODO : Choose your directories
SRC_DIR=./
OUT_DIR=../obj
OUT_BIN_DIR=../bin
ifndef CAPN
	CAPN=1
endif
ifndef PWRN
	PWRN=1
endif

CFLAGS=-O2 -std=c99 -Wall

all	:	$(TARGETS)

# General make
$(TARGETS)	:	$(OBJS) 
	@echo "building $* ... $(TARGETS)"
	@mkdir -p $(OUT_BIN_DIR)
	$(CC) $(CFLAGS) -o $(OUT_BIN_DIR)/$@ $(OBJS) $@.c

# Make yours if you define variables which is conflict with others or you want to name by your-self. 
scheduler-frfcfs	:	$(OBJS)
	@echo "building $* ..."
	@mkdir -p $(OUT_BIN_DIR)
	$(CC) $(CFLAGS) -DCAPN=$(CAPN) -o $(OUT_BIN_DIR)/$@-$(CAPN) $(OBJS) $@.c

scheduler-pwrdn	:	$(OBJS)
	@echo "building $* ..."
	@mkdir -p $(OUT_BIN_DIR)
	$(CC) $(CFLAGS) -DPWRN=$(PWRN) -o $(OUT_BIN_DIR)/$@-$(PWRN) $(OBJS) $@.c

$(OUT_DIR)/%.o	:	%.c
	@mkdir -p $(@D)
	$(CC) $(CFLAGS) -c $< -o $@

clean	:
	rm -rf $(OUT_DIR) $(OUT_BIN_DIR)

