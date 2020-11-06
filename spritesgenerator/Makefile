#---------------------------------------------------------------------------------
.SUFFIXES:
#---------------------------------------------------------------------------------

ifeq ($(strip $(DEVKITARM)),)
$(error "Please set DEVKITARM in your environment. export DEVKITARM=<path to>devkitARM")
endif

TOPDIR ?= $(CURDIR)
include $(DEVKITARM)/3ds_rules

#---------------------------------------------------------------------------------
TARGET		:=	$(notdir $(CURDIR))
GRAPHICS	:=	gfx
GFXBUILD	:=	out

#---------------------------------------------------------------------------------
# pas vraiment besoin de modifier quoi que ce soit au-delà de ce point, sauf si 
# vous devez ajouter desrègles pour différentes extensions de fichiers
#---------------------------------------------------------------------------------
ifneq ($(BUILD),$(notdir $(CURDIR)))
#---------------------------------------------------------------------------------

export OUTPUT	:=	$(CURDIR)/$(TARGET)
export TOPDIR	:=	$(CURDIR)

export VPATH	:=	$(foreach dir,$(GRAPHICS),$(CURDIR)/$(dir))

export DEPSDIR	:=	$(CURDIR)/$(BUILD)
GFXFILES	:=	$(foreach dir,$(GRAPHICS),$(notdir $(wildcard $(dir)/*.t3s)))

#---------------------------------------------------------------------------------
export T3XFILES	:=	$(patsubst %.t3s, $(GFXBUILD)/%.t3x, $(GFXFILES))
#---------------------------------------------------------------------------------
.PHONY: all clean

#---------------------------------------------------------------------------------
all: $(GFXBUILD) $(DEPSDIR) $(T3XFILES)
#---------------------------------------------------------------------------------
clean:
	@echo Nettoyage ...
	@rm -fr out/AmiiGhost.t3x
#---------------------------------------------------------------------------------
$(GFXBUILD)/AmiiGhost.t3x:	AmiiGhost.t3s
#---------------------------------------------------------------------------------
	@echo Compilation de AmiiGhost.t3x en cours ...
	@tex3ds -i $< -o $(GFXBUILD)/AmiiGhost.t3x
	@echo AmiiGhost.t3x compilé avec Succès!


#---------------------------------------------------------------------------------
.PRECIOUS	:	%.t3x
#---------------------------------------------------------------------------------
%.t3x:	%.t3s
#---------------------------------------------------------------------------------
	@echo $(notdir $<)
	@tex3ds -i $< -o $*.t3x

#---------------------------------------------------------------------------------------
endif
#---------------------------------------------------------------------------------------