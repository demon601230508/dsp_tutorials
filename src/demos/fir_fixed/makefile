# filenames with common base
EXE_BASE = demo_fir_fixed
EXE = $(EXE_BASE).exe

SRCS = \
./demo_fir_fixed.c 

LIBS = \

COMPILER = gcc

INCLUDES = \
    -I../../

LIBDIRS = \

# add lib directory paths to VPATH so that libraries can be used as a dependency
VPATH = \

DEFINES = \

OPTIONS = \

LINKOPTS = \

OBJ_DIR = objects

OBJS = $(patsubst %.c, $(OBJ_DIR)/%.o, $(notdir $(SRCS))) 

.PHONY: all clean cleanandbuild obj

# default rule is "all" since it is the first rule
all: $(EXE)

# clean and build
cleanandbuild: clean all

# rule to create object files folder
obj:
	mkdir -p $(OBJ_DIR)

.SECONDEXPANSION:
PERCENT = %

# pattern rule to build all object files
# the "obj" rule is always run
$(OBJS): %.o : $$(filter $$(PERCENT)/$$(notdir %).c, $(SRCS)) | obj
	@echo 'Building file: $<'
	@echo 'Invoking: C Compiler'
	$(COMPILER) $(DEFINES) $(INCLUDES) $(OPTIONS) -MMD -MP -MF"$(@:%.o=%.d)" -MT"$(@:%.o=%.o)" -MT"$(@:%.o=%.d)" -c $< -o $(OBJ_DIR)/$(notdir $@)
	@echo 'Finished building: $<'
	@echo ' '

# these are the rules for rebuilding the sources if header files change
DEPS = $(patsubst %.o, %.d, $(OBJS))
ifneq ($(MAKECMDGOALS),clean)
ifneq ($(strip $(DEPS)),)
-include $(DEPS)
endif
endif

# rule to build the final executable
$(EXE): $(OBJS) $(LIBS)
	@echo 'Building target: $@'
	@echo 'Invoking: Linker'
	$(COMPILER) $(LIBDIRS) $(LINKOPTS) -o "$(EXE)" $(OBJS) $(LIBS)
	@echo 'Finished building target: $@'
	@echo ' '

# Other Targets
RM := rm -rf
clean:
	-$(RM) $(OBJS) $(DEPS) $(EXE)
	-@echo ' '

