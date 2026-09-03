TESTS =
check_PROGRAMS =

# libcheck based unit tests, only built when libcheck was found
if HAVE_CHECK
TESTS += check_queue #check_checkpoint
check_PROGRAMS += check_queue #check_checkpoint

check_queue_SOURCES = check_queue.c $(top_srcdir)/libcircle/libcircle.h
check_queue_CFLAGS = -I$(top_srcdir)/libcircle/ @CHECK_CFLAGS@
check_queue_LDADD = $(top_builddir)/libcircle.la @CHECK_LIBS@

#check_checkpoint_SOURCES = check_checkpoint.c $(top_srcdir)/libcircle.h
#check_checkpoint_CFLAGS = -I$(top_srcdir)/libcircle/ @CHECK_CFLAGS@
#check_checkpoint_LDADD = $(top_builddir)/libcircle.la @CHECK_LIBS@
endif

# Regression test for blocking sends on the work transfer path.  Needs
# an MPI launcher rather than libcheck; the script skips itself when
# there is no launcher to run.
TESTS += deadlock_test.sh
check_PROGRAMS += check_deadlock

check_deadlock_SOURCES = check_deadlock.c $(top_srcdir)/libcircle/libcircle.h
check_deadlock_CFLAGS = -I$(top_srcdir)/libcircle/ $(MPI_CFLAGS)
check_deadlock_LDADD = $(top_builddir)/libcircle.la $(MPI_CLDFLAGS)

check_SCRIPTS = deadlock_test.sh
CLEANFILES = deadlock_test.sh
EXTRA_DIST = deadlock_test.sh.in

deadlock_test.sh: deadlock_test.sh.in Makefile
	$(AM_V_GEN)sed -e 's|@MPIRUN[@]|$(MPIRUN)|g' $(srcdir)/deadlock_test.sh.in > $@
	@chmod +x $@
