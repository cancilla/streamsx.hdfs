##################################################################### 
# Copyright (C)2014, International Business Machines Corporation and 
# others. All Rights Reserved. 
#####################################################################     
                            
.PHONY: all clean

SPLC_FLAGS = -a -z -t ../../com.ibm.streamsx.hdfs:$(STREAMS_INSTALL)/toolkits/com.ibm.streamsx.hdfs

SPLC = $(STREAMS_INSTALL)/bin/sc

SPL_CMD_ARGS ?=
SPL_COMP1NAME=Read
SPL_COMP2NAME=Write
SPL_MAIN_COMPOSITE1 = com.ibm.streamsx.hdfs.sample::$(SPL_COMP1NAME)
SPL_MAIN_COMPOSITE2 = com.ibm.streamsx.hdfs.sample::$(SPL_COMP2NAME)
STANDALONE_OUTPUT_DIR = output/Standalone
DISTRIBUTED_OUTPUT_DIR = output/Distributed

all: distributed

standalone:
	$(SPLC) $(SPLC_FLAGS) -T -M $(SPL_MAIN_COMPOSITE1) --output-dir ./$(STANDALONE_OUTPUT_DIR)/$(SPL_COMP1NAME) $(SPL_CMD_ARGS)
	$(SPLC) $(SPLC_FLAGS) -T -M $(SPL_MAIN_COMPOSITE2) --output-dir ./$(STANDALONE_OUTPUT_DIR)/$(SPL_COMP2NAME) $(SPL_CMD_ARGS)

distributed:
	$(SPLC) $(SPLC_FLAGS) -M $(SPL_MAIN_COMPOSITE1) --output-dir ./$(DISTRIBUTED_OUTPUT_DIR)/$(SPL_COMP1NAME) $(SPL_CMD_ARGS)
	$(SPLC) $(SPLC_FLAGS) -M $(SPL_MAIN_COMPOSITE2) --output-dir ./$(DISTRIBUTED_OUTPUT_DIR)/$(SPL_COMP2NAME) $(SPL_CMD_ARGS)

clean: clean-standalone clean-distributed

clean-standalone:
	$(SPLC) $(SPLC_FLAGS) -C -M $(SPL_MAIN_COMPOSITE1) --output-dir ./$(STANDALONE_OUTPUT_DIR)/$(SPL_COMP1NAME)
	$(SPLC) $(SPLC_FLAGS) -C -M $(SPL_MAIN_COMPOSITE2) --output-dir ./$(STANDALONE_OUTPUT_DIR)/$(SPL_COMP2NAME)
	-rm -rf toolkit.xml
	-rm -rf data/FileContents.txt
	-rm -rf data/FileContentsInputPort.txt	

clean-distributed:
	$(SPLC) $(SPLC_FLAGS) -C -M $(SPL_MAIN_COMPOSITE1) --output-dir ./$(DISTRIBUTED_OUTPUT_DIR)/$(SPL_COMP1NAME)
	$(SPLC) $(SPLC_FLAGS) -C -M $(SPL_MAIN_COMPOSITE2) --output-dir ./$(DISTRIBUTED_OUTPUT_DIR)/$(SPL_COMP2NAME)
	-rm -rf toolkit.xml
	-rm -rf data/FileContents.txt
	-rm -rf data/FileContentsInputPort.txt